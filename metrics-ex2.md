# Metrics - Exercice 2

J'ai choisi la fonction **withdrawMoney(double withdrawAmount)**.
1. `Cyclomatic complexity value` : **5**
```bash
~ public boolean isWithdrawable(double withdrawAmount): 5
```
```java
public boolean withdrawMoney(double withdrawAmount) {
    if (withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount < withdrawLimit
            && withdrawAmount + amountWithdrawn <= withdrawLimit) { // 4 Decisions (similar to a if(...) => return true, else if(...)  => return true, else if(...)  => return true, else if(...)  => return true, else => return false) 
        balance = balance - withdrawAmount;
        success = true;
        amountWithdrawn += withdrawAmount;
    } else { // 1 Decision
        success = false;
    }
    return success;
}
```

## Refactor

Dans un premier temps, pour réduire la complexité, nous pouvons supprimer la 3ème condition (**withdrawAmount < withdrawLimit**) étant donné qu'elle est indirectement testé dans la 4ème condition (**withdrawAmount + amountWithdrawn <= withdrawLimit**).
Puis, nous pouvons améliorer la lisibilité en retournant le résultat de la condition **isWithdrawable** dès le départ, ce qui évite d'avoir le code concernant le retrait dans la condition **if**.
Nous pouvons également extraire la logique de validation dans une autre méthode comme **isWithdrawable(double withdrawAmount)** afin de séparer les règles métier des modifications.
Cette refactorisation améliore la lisibilité, la testabilité et la maintenabilité de cette fonctionnalité.

`Which part would you extract into a helper method ?`
withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount < withdrawLimit && withdrawAmount + amountWithdrawn <= withdrawLimit

`What name would you give this helper ?`
isWithdrawable

`Implement the refactoring (create the helper method, simplify the original method).`

```java
public boolean withdrawMoney(double withdrawAmount) {
    if (!isWithdrawable(withdrawAmount)) { // 2 Decisions (similar to if(...) => return false, else => ...)
        return false;
    }
    balance = balance - withdrawAmount;
    amountWithdrawn += withdrawAmount;
    return true;
}

public boolean isWithdrawable(double withdrawAmount) {
    return withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount + amountWithdrawn <= withdrawLimit; // 4 decisions (similar to a if(...) => return true, else if(...)  => return true, else if(...)  => return true, else => return false) 
}
```

`Re-run CK Metrics on that file and check whether the complexity for that method decreased.`

```bash
~ public boolean withdrawMoney(double withdrawAmount): 2
~ public boolean isWithdrawable(double withdrawAmount): 4
```