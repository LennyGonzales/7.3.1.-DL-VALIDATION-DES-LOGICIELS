# Metrics - Exercice 4

`List 3 issues that you consider important (for example: potential bug, major code smell, suspicious condition). For each issue:`
**Found 144 issues in 11 files.**

1.
- Rule name : **Try-with-resources should be used**
- File and line : **Bank.java:144**
- Your explanation in your own words (2–3 lines) : Les ressources Java (fichiers, ...) doivent être fermées après usage pour libérer de la mémoire et éviter les fuites et les problèmes de mémoire. Sans **try-with-resources**, le système d'exploitation les garde occupés même si Java les croit libérés.

```java
public void saveAccounts(Bank accManager) {
		FileOutputStream fos = null;
		OutputStreamWriter osw = null;
		try {
			fos = new FileOutputStream("C:\\Users\\jay4k\\Desktop\\stuff\\Bankaccountinfo\\BankAccountinfotext.text");
			osw = new OutputStreamWriter(fos);
			for (int i = 0; i < Accounts.size(); i++) {
				BankAccount tmp = Accounts.get(i);

				osw.write(tmp.convertToText(tmp));

			}
		} catch (IOException e) {
			System.out.println("Error writing to file");
		} finally {
			if (osw != null) {
				try {
					osw.close();
				} catch (IOException e) {
					// no action
				}
			}
			if (fos != null) {
				try {
					fos.close();
				} catch (IOException e) {
					// no action
				}
			}
		}
	}
```
Correction :
Nous déclarons les variables **fos** et **osw** dans les parenthèses du **try** (try-with-resources). Ainsi, les variables vont être nettoyer automatiquement (plus besoin du block finally).
```java
public void saveAccounts(Bank accManager) {
		try (
			FileOutputStream fos = new FileOutputStream("C:\\Users\\jay4k\\Desktop\\stuff\\Bankaccountinfo\\BankAccountinfotext.text");
			OutputStreamWriter osw = new OutputStreamWriter(fos)
		) {
			for (int i = 0; i < Accounts.size(); i++) {
				BankAccount tmp = Accounts.get(i);

				osw.write(tmp.convertToText(tmp));

			}
		} catch (IOException e) {
			System.out.println("Error writing to file");
		}

	}
```

2.
- Rule name : **String literals should not be duplicated**
- File and line : **BankAccountApp.java:96,160,197**
- Your explanation in your own words (2–3 lines) : Répéter les mêmes chaînes de caractères partout complique les modifications futures (si on veut changer la valeur d'une chaîne de caractères, il va falloir modifier dans plusieurs endroits dans le projet, avec un risque d'oubli ou d'erreur). Il est préférable de les mettre dans une constante pour définir sa valeur dans un seul endroit.

```java
public class BankAccountApp {
	public static void main(String[] args) {
        ...
        if (operation.equalsIgnoreCase("DEPOSIT")) {
        ...
        if (operation.equalsIgnoreCase("DEPOSIT")) {
        ...
        if (!operation.equalsIgnoreCase("BALANCE") && !operation.equalsIgnoreCase("DEPOSIT")
        ...
    }
}
```
Correction:
```java
public class BankAccountApp {
	private static final String DEPOSIT = "DEPOSIT";

    public static void main(String[] args) {
        ...
        if (operation.equalsIgnoreCase(DEPOSIT)) {
        ...
        if (operation.equalsIgnoreCase(DEPOSIT)) {
        ...
        if (!operation.equalsIgnoreCase("BALANCE") && !operation.equalsIgnoreCase(DEPOSIT)
        ...
    }
}
```

3.
- Rule name : **Cognitive Complexity of methods should not be too high**
- File and line : **BankAccountApp.java:96**
- Your explanation in your own words (2–3 lines) : Le main de la classe **BankAccountApp** a une complexité cognitive trop élevée à cause des boucles imbriquées (**while dans while**), des **if dans des if**. Cela rend le flux du programme très difficile à suivre mentalement. Il faudrait extraire les menus et les opérations dans des méthodes séparées pour réduire cette complexité et rendre le code plus lisible, mais surtout maintenable et testable.

`Re-run SonarLint on the same scope and confirm:`

**Found 142 issues in 11 files.**
Je peux constater que les 2 issues que j'ai réparé ne sont plus présentes dans le rapport de SonarQube.

`In 3–4 lines:
Do SonarLint issues appear more often in the classes with higher WMC / CBO you saw earlier, or not really?`

Il n'y a pas de réelle corrélation entre un haut WMC/CBO et le nombre d'issues.
Par exemple, la classe **BankAccountApp** a WMC=2 et CBO=3 alors qu'elle a 47 issues.
Alors que la classe **Person** a WMC=23 et CBO=3 possède seulement 9 issues.
