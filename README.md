

q1: Quelles sont les structures de données à utiliser ?

Les principales structures de données utilisées dans le code sont les matrices globales B, C, et D (resultat de b*c), représentées comme des tableaux d'entiers. En outre, deux structures personnalisées sont utilisées :

argument, qui est utilisée pour passer des arguments aux threads.
buffer, qui est utilisée comme un tampon partagé entre les threads producteurs et consommateurs. Cette structure a trois champs :
val, qui contient le résultat du produit.
cas, qui est -1 si la valeur a été consommée et contient le numéro de colonne où placer le résultat lorsque le producteur la génère.
i, qui contient le numéro de ligne où le résultat doit être placé dans la matrice D.

q2: Comment allez-vous protéger l'accès à ces données?
  protege l indice j:
Pour éviter le remplacement de numéros de colonne non consommés dans le buffer, chaque thread producteur utilise une boucle infinie jusqu'à ce que le numéro de colonne soit consommé. Le thread producteur effectue des sem_post à chaque itération pour éviter tout blocage potentiel du programme. De manière similaire, le thread consommateur entre également dans une boucle infinie où, à chaque itération, il vérifie si t.cas n'est pas égal à -1. Dès qu'un numéro de colonne est disponible, le consommateur le récupère, le consomme, puis met à jour la valeur de t.cas à -1. Cette approche permet au producteur d'utiliser la même case du buffer pour stocker un autre résultat une fois qu'il a été consommé par le consommateur. Les opérations de sem_post dans les boucles infinies garantissent la fluidité de la communication entre les threads producteurs et consommateurs, évitant ainsi tout blocage potentiel du programme.

  protege la ligne envoyer dans l argument a:
  Cette structure est modifiée pour être un tableau d'arguments argument a[n], chaque élément contenant les détails pour un thread spécifique.

q3- quels sont les risques?
Accès Concurrent aux Matrices
Utilisation courante des variables globales
Écraser les valeurs inutilisées enregistrées dans le tampon


Ces risques ont été résolus
