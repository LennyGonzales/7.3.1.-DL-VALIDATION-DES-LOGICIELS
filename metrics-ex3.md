# Metrics - Exercice 3

| Class |	LOC           | WMC |	CBO |	LCOM                        | Quick Notes |
|-------|-----------------|-----|-------|-------------------------------|-------------|
|Bank	| 412  | 14     |	 4	| 0 | - |
|BankAccount | 462 |	21	 | 3 |	46 | - |
|Person	| 324 | 23 |	3	| 79 | - |
|BankAccountApp	| 482 | 2 |	3 |	1 | - |

`Which class has the highest WMC?` => La classe Person possède le plus haut WMC.

`Which class has the highest CBO?` => La classe Bank possède le plus haut CBO.

`Looking at WMC + CBO + LCOM together. Which one class would you worry about most for future maintenance, and why?`

La classe Person serait la plus inquiétante pour la maintenance future.
En effet, elle possède un **WMC élevé** (23 méthodes, ainsi, elle a une plus grande complexité et les méthodes complexes ont tendance à être plus soumises aux erreurs), un **LCOM élevé** (79, ainsi, elle a une faible cohésion).