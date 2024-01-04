# Loan-duration
Ce projet Python a été créé dans le cadre de mes études en ingénierie financière pour automatiser le calcul de la durée des emprunts à partir d'un fichier CSV. L'application utilise l'interface graphique Tkinter pour simplifier l'interaction avec l'utilisateur.

Instructions d'utilisation
L'interface demande à l'utilisateur de placer le fichier CSV dans le même répertoire que le script Python et d'entrer son nom avec l'extension.
Le script utilise la bibliothèque chardet pour détecter automatiquement l'encodage du fichier CSV, puis crée une classe Dataset pour stocker les données du fichier.
La classe Calculation effectue le calcul de la durée des emprunts en fonction des informations du fichier CSV. Elle vérifie également l'éligibilité en fonction de la durée.
Les résultats sont enregistrés dans un nouveau fichier CSV appelé 'loan_results.csv' avec les colonnes 'Loan', 'Duration in years' et 'Eligibility'.

