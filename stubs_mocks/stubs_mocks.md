!SLIDE bullets incremental

# CTransakcjaBazowa #

  * db transaction support
  * rollback
  * commit
  * obviously db dependent
  * stubbed implementation


!SLIDE code smaller

    @@@ Java
    @MockClass(realClass = CTransakcjaBazowa.class)
    public class CTestTransakcjaBazowa {

        private boolean czyCommit;
        private boolean czyRollback;


        @Mock
        public void commit() throws CDBException { 
            czyCommit = true; 
        }

        @Mock
        public void rollback() throws CDBException {
            if(isNotCommited()) {
                czyRollback = true;
            }
        }

        @Mock
        public boolean isCommited() { return czyCommit; }

        @Mock
        public boolean isNotCommited() { return !isCommited(); }

        @Mock
        public boolean isRolledback() { return czyRollback; }

    }

!SLIDE bullets incremental

# CTransakcja #

  * db session management
  * Mockito mock for db session
  * obviously db dependent

!SLIDE code smaller

    @@@ Java
    @MockClass(realClass = CTransakcja.class)
    public class CTestTransakcja {

        private CSesjaDB sesjaMock;


        @Mock
        public CTestTransakcja() { }


        @Mock
        public CSesjaDB getSesja() {
            if (sesjaMock == null) {
                sesjaMock = Mockito.mock(CSesjaDB.class);

                when(sesjaMock.registerObject(anyObject())).
                    thenAnswer(
                        new Answer<Object>() {
                            @Override
                            public Object answer(
                                    InvocationOnMock invocation) {
                                return invocation.getArguments()[0];
                            }
                        });
            }

            return sesjaMock;
        }

    }

!SLIDE bullets incremental

# CEnumDB #

  * database dependent
  * untestable description
  * stubbed implementation


!SLIDE code

    @@@ Java
    @MockClass(realClass = CEnumDB.class)
    public class CTestEnumDB {

        @Mock
        public static boolean getCzyEnumBazyDanych() {
            return false;
        }

    }

