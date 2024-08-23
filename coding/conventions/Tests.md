---
tags:
  - coding
  - conventions
  - test
---
# Test Naming conventions

É raccomandato l'utilizzo della convenzione nel nominare i test nel seguente modo:
- Il nome del test dovrebbe esprimere un requisito specifico.
- Il nome del test dovrebbe includere l'input e lo stato desiderato in uscita.
- Il nome del test si dovrebbe presentare come fato di vita che esprime il workflow e le uscite.
- Il nome del test dovrebbe includere il nome del metodo testato.

## Qualche Esempio
**MethodName_StateUnderTest_ExpectedBehavior**
cons: should be renamed if method change name
example: isAdult_AgeLessThan18_False

**MethodName_ExpectedBehavior_StateUnderTest**
cons: should be renamed if method change name
example: isAdult_False_AgeLessThan18

**testFeatureBeingTested**
cons: “test” prefix is redundant
example: testIsNotAnAdultIfAgeLessThan18

**FeatureToBeTested**
cons: no clue what result is expected from name
example: IsNotAnAdultIfAgeLessThan18

**Should_ExpectedBehavior_When_StateUnderTest**
cons: duplicates `should` and `when`, long name
example: Should_ThrowException_When_AgeLessThan18

**When_StateUnderTest_Expect_ExpectedBehavior**
cons: duplicates `when` and `expect`
example: When_AgeLessThan18_Expect_isAdultAsFalse

**Given_Preconditions_When_StateUnderTest_Then_ExpectedBehavior — Behavior-Driven Development** (BDD)
cons: duplicates `given`, `when`, `then`; really long names
example: Given_UserIsAuthenticated_When_InvalidAccountNumberIsUsedToWithdrawMoney_Then_TransactionsWillFail