#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Définition de la structure de l'étudiant
struct Student {
    int id;
    char name[50];
    float grade;
};

// Prototypes des fonctions (le plan du programme)
void ajouterEtudiant();
void afficherEtudiants();
void rechercherEtudiant();

int main() {
    int choix;

    do {
        printf("\n========================================");
        printf("\n   SYSTEME DE GESTION DES ETUDIANTS");
        printf("\n========================================");
        printf("\n1. Ajouter un etudiant");
        printf("\n2. Afficher tous les etudiants");
        printf("\n3. Rechercher un etudiant par ID");
        printf("\n4. Quitter");
        printf("\n----------------------------------------");
        printf("\nVotre choix : ");
        
        // Sécurité pour la saisie du choix
        if (scanf("%d", &choix) != 1) {
            printf("\nErreur : Veuillez entrer un nombre valide.\n");
            while (getchar() != '\n'); // Vider le tampon en cas d'erreur
            continue;
        }

        switch (choix) {
            case 1:
                ajouterEtudiant();
                break;
            case 2:
                afficherEtudiants();
                break;
            case 3:
                rechercherEtudiant();
                break;
            case 4:
                printf("\nFermeture du programme. Au revoir !\n");
                break;
            default:
                printf("\nChoix invalide, veuillez recommencer.\n");
        }
    } while (choix != 4);

    return 0;
}

// Fonction pour ajouter un étudiant dans le fichier
void ajouterEtudiant() {
    FILE *file = fopen("students.txt", "a"); // "a" pour ajouter sans effacer
    struct Student s;

    if (file == NULL) {
        printf("\nErreur : Impossible d'ouvrir le fichier.\n");
        return;
    }

    printf("\n--- Ajouter un nouvel etudiant ---");
    printf("\nID : ");
    scanf("%d", &s.id);
    
    while (getchar() != '\n'); // Nettoyer le tampon (évite de sauter le nom)

    printf("Nom : ");
    scanf("%49s", s.name); // Limite à 49 caractères pour la sécurité

    printf("Note : ");
    scanf("%f", &s.grade);

    // Enregistrement formaté dans le fichier
    fprintf(file, "%d %s %.2f\n", s.id, s.name, s.grade);
    
    fclose(file);
    printf("\nSucces : L'etudiant a ete enregistre.\n");
}

// Fonction pour lire et afficher le contenu du fichier
void afficherEtudiants() {
    FILE *file = fopen("students.txt", "r"); // "r" pour lecture seule
    struct Student s;

    if (file == NULL) {
        printf("\nAucune donnee trouvee. Le fichier n'existe pas encore.\n");
        return;
    }

    printf("\n--- Liste des Etudiants ---");
    printf("\nID\tNOM\t\tNOTE");
    printf("\n----------------------------\n");

    // Lecture ligne par ligne jusqu'à la fin du fichier (EOF)
    while (fscanf(file, "%d %s %f", &s.id, s.name, &s.grade) != EOF) {
        printf("%d\t%s\t\t%.2f\n", s.id, s.name, s.grade);
    }

    fclose(file);
}

// Fonction pour rechercher un étudiant spécifique
void rechercherEtudiant() {
    FILE *file = fopen("students.txt", "r");
    struct Student s;
    int idRecherche, trouve = 0;

    if (file == NULL) {
        printf("\nErreur : Aucun fichier de donnees.\n");
        return;
    }

    printf("\nEntrez l'ID de l'etudiant a rechercher : ");
    scanf("%d", &idRecherche);

    while (fscanf(file, "%d %s %f", &s.id, s.name, &s.grade) != EOF) {
        if (s.id == idRecherche) {
            printf("\nEtudiant trouve !");
            printf("\nID    : %d", s.id);
            printf("\nNom   : %s", s.name);
            printf("\nNote  : %.2f\n", s.grade);
            trouve = 1;
            break; // On arrête la boucle dès qu'on a trouvé
        }
    }

    if (!trouve) {
        printf("\nAucun etudiant avec l'ID %d n'a ete trouve.\n", idRecherche);
    }

    fclose(file);
}
