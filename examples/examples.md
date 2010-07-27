!SLIDE bullets incremental

  * JUnit4 == any superclass for tests
  * Own superclass for mock injection related tasks


!SLIDE code smaller

    @@@ Java
    public abstract class CHipotekaTestBazowy {

        @MockClass(realClass = 
            CIntegracjaParametryzacjaBiznesowaProduktDefinicjaPulpit.class)
        public static class CGetInstance {
            @Mock
            public static IParametryzacjaBiznesowaProduktDefinicjaUsluga 
                    getInstance() {
                return null;
            }
        }


        @BeforeClass
        public static void setUpClass() {
            Mockit.setUpMocks(
                CGetInstance.class,
                CTestTransakcjaBazowa.class,
                CTestTransakcja.class,
                CTestEnumDB.class);
        }

        @Before
        public void setUpMocks() {
            MockitoAnnotations.initMocks(this);
        }

    }

!SLIDE code smaller

    @@@ Java
    public class CLogikaKredytHipotecznyTest extends CHipotekaTestBazowy {


        @InjectMocks
        private CLogikaKredytHipoteczny logika = 
            CLogikaKredytHipoteczny.getInstance();



        @Mock
        private ILogikaDyspozycje logikaDyspozycje;

        @Mock
        private IBezpieczenstwo bezpieczenstwo;

        @Mock
        private ILogikaPomocnikUmowaPozyczka logikaPomocnikUmowaPozyczka;

        @Mock
        private ILogikaUmowaDEF logikaUmowaDEF;

        @Mock
        private ILogikaUmowaProdukt logikaUmowaProdukt;


        {...}

    }


!SLIDE bullets incremental

# Verification of method invocation #

  * was other logic invoked with apropriate args?
  * test fails if verification conditions aren't met


!SLIDE code smaller

    @@@ Java
    @Test
    public void nieaktywnaDyspozycjaWakacje () {
        assertThat(
            logika.czyAktywnaDyspozycjaWakacje(new CKredytHipoteczny()), 
            is(false));

        verify(logikaDyspozycje).pobierzDyspozycjaWakacjeAktywna(
            any(CKredytHipoteczny.class));
    }


!SLIDE bullets incremental

# Stubbing return values #

  * easy way of stubbing with Mockito
  * without method-rename problem (JMock)


!SLIDE code smaller

    @@@ Java
    @Test
    public void aktywnaDyspozycjaWakcje() {
        when(logikaDyspozycje.pobierzDyspozycjaWakacjeAktywna(
            any(CKredytHipoteczny.class))).
            thenReturn(new CDyspozycjaKredytHipotecznyWakacje());

        assertThat(
            logika.czyAktywnaDyspozycjaWakacje(new CKredytHipoteczny()), 
            is(true));
    }


!SLIDE code smaller

    @@@ Java
    @Test
    public void dodajKontoDlaNowaUmowaPosrednik() throws Exception {
        CKlient klient = new CKlient();

        CPromesaKredytHipoteczny promesa = new CPromesaKredytHipoteczny();

        CKredytHipoteczny umowa = new CKredytHipoteczny();
        umowa.setGlownyKredytobiorca(klient);

        CUmowaProdukt umowaKonto = new CUmowaProdukt();

        when(logikaPomocnikUmowaPozyczka.przygotujUmoweROR(
            (ISesja) any(),
            same(klient),
            same(promesa))).
            thenReturn(
                new CWynikPodpisanoUmoweProdukt(umowaKonto, klient));


        logika.dodajKontoDlaNowaUmowaPosrednik(umowa, promesa);

        assertThat(promesa.getCzyKontoAutomatyczne(), is(true));
        assertFalse(promesa.getCzyPodpisanaUmowaKontoAutomatyczne());

        verify(logikaUmowaProdukt).znajdzUmowaPoIdDef(
            eq(umowaKonto.getIdDEF()),
            any(List.class));
    }

