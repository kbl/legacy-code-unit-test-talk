!SLIDE bullets incremental

# Test frameworks #

  * <a href="http://junit.org">JUnit</a>
  * <a href="http://mockito.org">Mockito</a>
  * <a href="http://code.google.com/p/jmockit/">JMockit</a>
  * <a href="http://code.google.com/p/hamcrest/">hamcrest</a>


!SLIDE bullets incremental

# JUnit #

  * v4.8.2
  * @Test, @Before
  * @Test(expected = ClassCastException.class)
  * assertThat


!SLIDEi center bullets incremental

# Mockito #

![Mockito logo](mockito.jpg)

  * Mockito.mock(Interface.class)
  * Mockito.verify(mock).interfaceMethod()
  * ArgumentCaptor<Type>


!SLIDE bullets incremental

# JMockit #

  * TODO


!SLIDE code

# hamcrest #

    @@@ Java
    assertTrue(condition);
    assertThat(condition, is(true));

    assertEquals(expected, actual);
    assertThat(expected, is(actual));
    assertThat(expected, is(equalTo(actual)));
    assertThat(expected, equalTo(actual));

    assertTrue(list.contains(element));
    assertThat(list, contains(element));

