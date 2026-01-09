# Metrics - Exercice 1

Command : `java -jar ./ckjm_ext.jar ./target/classes/bankAccountApp/*.class`

| Class |	LOC (approx.) |	NOM |	Short description of responsibility |
|-------|-----------------|-----|---------------------------------------|
|Bank	|       413       |	 14	| Responsable de la création, de la suppression, de la recherche, de l'enregistrement, du chargement des comptes, de ... et du virements entre les comptes. |
|BankAccount |	462	 | 20 |	Responsable du stockage des données de compte et de leur gestion (dépôts, retraits, solde). |
|Person	| 325 |	23	| Responsable de la conservation et de la validation des informations personnelles. |
|BankAccountApp	| 491 |	2 |	Responsable de toute la logique d’IHM console : menus, boucles, lecture de saisies, choix d’opérations, gestion des erreurs, ... |


`⇒ Do you feel its size roughly matches its responsibility?`

Pour Bank, la taille est globalement cohérente avec sa responsabilité de gestion centrale des comptes (création, recherche, stats, persistance).
Pour BankAccount, la taille se justifie par le mélange données métier + opérations (dépôt/retrait) + sérialisation, même si la serialisation/desarialisation pourrait être extrait.
Pour Person, la taille paraît raisonnable si la classe fait à la fois stockage et validation détaillée des données personnelles.
Pour BankAccountApp, il n’y a quasiment que la fonction **main**, donc la métrique indique clairement que trop de logique applicative et de gestion de cas d’usage est concentrée dans cette seule méthode. Il faudrait répartir la logique (menus, lecture/saisie, ...) dans d’autres classes et réduire main à un simple démarrage de l’application.
