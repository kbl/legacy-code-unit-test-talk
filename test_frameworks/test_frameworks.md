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


!SLIDE center bullets incremental

# Mockito #

![Mockito logo](mockito.jpg)

  * Mockito.mock(Interface.class)
  * Mockito.verify(mock).interfaceMethod()
  * ArgumentCaptor<Type>


!SLIDE bullets incremental

# JMockit #

  * constructors mocking
  * static methods mocking
  * well integrate with Mockito


!SLIDE bullets incremental

# hamcrest #

  * readable assertions
  * easy tests of collections inclusion/eclusion
  * could be used with standard JUnit asserts

!SLIDE code incremental

# hamcrest example #

    @@@ Java
    assertTrue(condition);
    assertThat(condition, is(true));

    assertEquals(expected, actual);
    assertThat(expected, is(actual));
    assertThat(expected, is(equalTo(actual)));
    assertThat(expected, equalTo(actual));

    assertTrue(list.contains(element));
    assertThat(list, contains(element));

