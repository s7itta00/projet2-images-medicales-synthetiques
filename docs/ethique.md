# Réflexion éthique et fiche du modèle

## Fiche du modèle

| Élément | Description |
|---|---|
| Modèles | CVAE conditionnel (latent 64) et GAN conditionnel (hinge loss + spectral norm) |
| Entrée | Une classe (0 à 6) + un bruit aléatoire |
| Sortie | Une image de dermoscopie synthétique RGB 64 × 64 |
| Données d'entraînement | DermaMNIST, 7 007 images (licence CC BY-NC 4.0) |
| Usage prévu | Recherche et enseignement : étude de l'augmentation de données pour une classe rare |
| Usage interdit | Diagnostic médical, publication d'images synthétiques présentées comme réelles, usage commercial |
| Qualité mesurée | FID 212,5 (CVAE) et 336,2 (GAN), contre 13,5 pour vraies vs vraies |

## Points éthiques

1. **Marquage des images.** Chaque image produite par la démo porte un bandeau rouge « SYNTHÉTIQUE - IA ». Une image synthétique ne doit jamais pouvoir être confondue avec une vraie photo de patient.

2. **Aucun usage diagnostique.** Les modèles et les classifieurs de ce projet ne sont pas validés cliniquement. Le meilleur classifieur ne retrouve en moyenne que 67 % des dermatofibromes du test, avec une forte variabilité. Ils ne doivent jamais servir à poser un diagnostic.

3. **Vie privée et mémorisation.** Un générateur qui recopie ses images d'entraînement pourrait révéler des données de patients. Nous l'avons vérifié avec la distance au plus proche voisin :
   - **GAN** : 0 % d'images suspectes ;
   - **CVAE** : 4,3 % d'images suspectes. Ce chiffre s'explique par le flou de ses images : à l'inspection visuelle, elles sont différentes des images d'entraînement.

   Ce test ne remplace pas une garantie formelle comme la confidentialité différentielle.

4. **Biais des données.** DermaMNIST (HAM10000) contient surtout des **peaux claires** et provient de deux centres seulement (Autriche, Australie). Les images générées héritent de ce biais. Un modèle entraîné dessus risque d'être moins fiable pour les peaux foncées.

5. **Fausse impression de progrès.** Les images synthétiques peuvent donner l'illusion de « plus de données ». Nos résultats montrent qu'elles **ne remplacent pas** les vraies images : en TSTR, le rappel de la classe 3 est de 0. Avec seulement 23 images de classe 3 dans le test, il faut aussi rester prudent dans l'interprétation des chiffres.

6. **Séparation stricte des données.** Les images synthétiques sont ajoutées uniquement à l'entraînement. La validation et le test ne contiennent que de vraies images.

7. **Licence.** DermaMNIST est sous licence CC BY-NC 4.0. Ce projet est non commercial et cite les sources (voir `data/README.md`).
