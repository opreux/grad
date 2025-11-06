# TP d'introduction à PHP - Site Vitrine GRAD

## Objectifs pédagogiques

Ce TP vous permettra de découvrir PHP, un langage de programmation côté serveur, en transformant progressivement un site web statique en site dynamique. Vous apprendrez les concepts fondamentaux de PHP : inclusion de fichiers, boucles, traitement de formulaires et interaction avec une base de données.

## Introduction

### Qu'est-ce que PHP ?

PHP (Hypertext Preprocessor) est un langage de programmation côté serveur. Contrairement aux langages côté client comme JavaScript, PHP s'exécute sur le serveur web avant que la page ne soit envoyée au navigateur.

**Point important** : Le client (votre navigateur) ne reçoit jamais le code PHP, uniquement le résultat HTML généré par PHP. Vous pouvez le vérifier en affichant le code source d'une page PHP dans votre navigateur : vous ne verrez que du HTML.

### Vérification de l'environnement de travail

Avant de commencer, vérifions que votre environnement PHP est correctement configuré.

1. Créez un fichier nommé `test.php` dans votre dossier `public_html`
2. Ajoutez le code suivant dans ce fichier :

```php
<?php
    phpinfo();
?>
```

3. Accédez à ce fichier via votre navigateur à l'adresse : `http://localhost/~identifiant/test.php` (en remplaçant identifiant par votre identifiant de connexion au réseau local).
4. Vous devriez voir s'afficher une page contenant toutes les informations de configuration PHP

Si cette page s'affiche correctement, votre environnement est prêt. Supprimez ensuite ce fichier `test.php` pour des raisons de sécurité.

---

## Étape 1 : Inclusion de texte avec PHP

### Objectif

Utiliser PHP pour insérer dynamiquement le contenu texte de la page d'accueil.

### Instructions

1. Ouvrez le fichier `page_d_accueil.html` et repérez le contenu textuel principal (lignes 29-41). Il s'agit du texte présent dans la div `descetp`.

2. Extrayez ce texte et créez un nouveau fichier nommé `accueil.txt` contenant uniquement le texte suivant :

```
GRAD, VOTRE SPÉCIALISTE BOIS<br>
La société grad est une entreprise de création d'équipements extérieurs implantée depuis 1988 en Alsace, au Nord de Strasbourg.<br>
Spécialisée dans les aménagements extérieurs en mix-matières bois, grès cérame, aluminium, Inox, verre… et pionniers dans la terrasse, nous occupons depuis 2005 la place de leader national dans ce domaine.<br>
« Nous occupons depuis 2005 la place de leader national »<br>
Notre savoir-faire et notre esprit d'innovation nous valent une réputation d'excellence qui dépasse les frontières du pays avec de nombreux concepts brevetés.<br>
Le développement européen est en cours avec déjà des implantations fortes en Allemagne, Autriche, Suisse et Belgique.<br>
Forts de plus de 25 années expériences,nous pouvons aujourd'hui prétendre apporter la solution aux demandes les plus pointues, les plus originales, les plus novatrices…<br>
La prise de participation par l'entreprise alsacienne Burger, depuis avril 2016, nous permettra d'atteindre le très haut niveau de notoriété qui nous revient dans le domaine de l'aménagement de terrasse.<br>
grad c'est qui ?<br>
C'est 49 collaborateurs au siège alsacien (production, logistique, administration,…).<br>
C'est un réseau de près de 100 partenaires formés, répartis dans toute la France pour poser nos produits, chez vous.
C'est de nombreux partenaires à l'étranger pour des chantiers jusqu'au bout du monde !<br>
```

3. Renommez `page_d_accueil.html` en `page_d_accueil.php`

4. Dans le fichier `page_d_accueil.php`, remplacez le contenu de la div `descetp` (lignes 28-41) par :

```php
<div id ="descetp">
    <?php include 'accueil.txt'; ?>
</div>
```

5. Testez votre page en accédant à `page_d_accueil.php` via votre navigateur. Le texte doit s'afficher normalement.

**Note** : La fonction `include` permet d'insérer le contenu d'un fichier dans un autre fichier PHP au moment de l'exécution.

---

## Étape 2 : Inclusion des textes de la page "Nos prestations"

### Objectif

Appliquer la même technique d'inclusion pour les textes de la page "Nos prestations".

### Instructions

1. Ouvrez le fichier `nos_prestations.html` et repérez les 5 textes de prestations :
   - Les aménagements d'espace (lignes 30-35)
   - Les escaliers (lignes 42-48)
   - Les garde-corps (lignes 55-61)
   - Les palissades (lignes 68-74)
   - Les planchers (lignes 81-87)

2. Créez 5 fichiers texte correspondants : `prestation1.txt` etc.

3. N'oubliez pas de renommer `nos_prestations.html` en `nos_prestations.php`

4. Remplacez chaque bloc de texte par une inclusion PHP.

---

## Étape 3 : Création d'un header réutilisable

### Objectif

Créer un fichier header réutilisable pour éviter la duplication de code dans chaque page.

### Instructions

1. Examinez le header de n'importe quelle page HTML. Vous constaterez qu'il est identique sur toutes les pages (logo, menu de navigation).

2. Créez un nouveau fichier `header.php` contenant le code du header :

```php
<header>
    <p><h2><?php echo $titre_page; ?></h2>
        <div id="bandeaulogo">
            <img class="photo" src="logo_grad.jpg" alt="Logo" width="80" height="40">
        </div>
        <div id="menu">
            <a href="page_d_accueil.php" class="menuopt">Page d'accueil</a>
            <a href="nos_prestations.php" class="menuopt">Nos Prestations</a>
            <a href="nos_produits.php" class="menuopt">Nos Produits</a>
            <a href="nos_realisations.php" class="menuopt">Nos Réalisations</a>
            <a href="contact.php" class="menuopt">contact</a>
        </div>
    </p>
</header>
```

**Note** : Remarquez l'utilisation de `<?php echo $titre_page; ?>` pour afficher un titre dynamique.

3. Dans chaque page PHP (`page_d_accueil.php`, `nos_prestations.php`, etc.), remplacez le bloc `<header>...</header>` par :

```php
<?php
    $titre_page = "Page d'accueil"; // Adaptez le titre selon la page
    include 'header.php';
?>
```

4. N'oubliez pas de mettre à jour les liens dans le menu pour pointer vers les fichiers `.php` au lieu de `.html`.

5. Testez toutes vos pages pour vérifier que le header s'affiche correctement.

---

## Étape 4 : Utilisation de boucles pour les prestations

### Objectif

Découvrir les boucles en PHP pour afficher les prestations de manière dynamique.

### Instructions

1. Créez un fichier `prestations.php` qui contiendra un tableau associatif avec toutes les informations des prestations :

```php
<?php
$prestations = array(
    array(
        'titre' => 'LES AMÉNAGEMENTS D\'ESPACE',
        'texte' => 'S\'il y a bien des détails qu\'il ne faut pas négliger, ce sont bien ceux qui constituent votre extérieur. Des bacs à plantes aux carrés potagers, des mobiliers de jardin à la cabane pour enfants, nos collections apporteront à la fois une ambiance chaleureuse et un cadre moderne.',
        'image' => 'amenagement.jpg',
        'alt' => 'Prestation 1'
    ),
    array(
        'titre' => 'LES ESCALIERS',
        'texte' => 'Véritable lieu de passage, l\'escalier grad a été pensé pour vous simplifier la vie. À lui seul, il satisfait toutes les attentes que vous pourriez avoir : robustesse, stabilité et élégance. Sa surface rainurée lui confère une adhérence à toute épreuve. Adaptable en longueur et en largeur, il vous offrira un confort de déplacement très appréciable au quotidien.',
        'image' => 'escalier-GC.jpg',
        'alt' => 'Prestation 2'
    ),
    array(
        'titre' => 'LES GARDE-CORPS',
        'texte' => 'Allier la sécurité et l\'esthétique, tel est le défi que nous avons relevé et que nous vous proposons de découvrir à travers notre vaste choix de garde-corps. Du classique au contemporain, avec des barres ou des câbles, en bois, Inox, verre ou panneaux, vous trouverez forcément votre bonheur parmi nos propositions sur mesure.',
        'image' => 'GC.jpg',
        'alt' => 'Prestation 3'
    ),
    array(
        'titre' => 'LES PALISSADES',
        'texte' => 'Pour disposer de votre terrasse, à l\'abri des regards indiscrets ou du vent, nous vous proposons un vaste choix de palissades en bois. Ces dernières pourront également être utilisées pour délimiter votre parcelle. Nos différents modèles sauront vous séduire par leur allure et leur solidité qui seront préservées au fil du temps.',
        'image' => 'palissade.jpg',
        'alt' => 'Prestation 4'
    ),
    array(
        'titre' => 'LES PLANCHERS (TERRASSES BOIS)',
        'texte' => 'À la pointe de la technologie en matière de préservation du bois, les planchers grad ont été pensés pour satisfaire vos envies. Dotés d\'un système de pose breveté, d\'une fixation invisible et démontable, ils s\'adaptent aux particularités de votre terrasse. Issus de forêts bien gérées, nos matériaux sont sélectionnés pour vous garantir des terrasses de qualité : imputrescibles, stables et pérennes.',
        'image' => 'terrasse.jpg',
        'alt' => 'Prestation 5'
    )
);
?>
```

2. Dans le fichier `nos_prestations.php`, remplacez tous les blocs de prestations par une boucle :

```php
<?php include 'prestations.php'; ?>

<?php
foreach ($prestations as $prestation) {
    echo '<div id="prestations">';
    echo '<br>' . $prestation['titre'] . '<br>';
    echo $prestation['texte'] . '<br></div>';
    echo '<div id="amenagement">';
    echo '<img class="photo" src="' . $prestation['image'] . '" alt="' . $prestation['alt'] . '" width="300" height="150">';
    echo '</div>';
}
?>
```

**Explication** : La boucle `foreach` parcourt chaque élément du tableau `$prestations`. Pour chaque prestation, elle affiche le titre, le texte et l'image.

3. Testez votre page `nos_prestations.php`. Vous devriez voir les 5 prestations s'afficher correctement.

---

## Étape 5 : Application des boucles pour les produits

### Objectif

Appliquer la même technique de boucle pour la page "Nos produits".

### Instructions

1. Créez un fichier `produits.php` contenant un tableau avec les informations des 5 produits :

```php
<?php
$produits = array(
    array(
        'nom' => 'LE DOUGLAS',
        'description' => 'Cliquez sur l\'image a droite pour afficher les informations sur le bois douglas.',
        'image' => 'douglas.jpg',
        'lien' => 'douglas.html',
        'alt' => 'Produit 1'
    ),
    array(
        'nom' => 'L\'ACCOYA',
        'description' => 'Cliquez sur l\'image a droite pour afficher les informations sur le bois accoya.',
        'image' => 'accoya.jpg',
        'lien' => 'accoya.html',
        'alt' => 'Produit 2'
    ),
    array(
        'nom' => 'LE THERMOFRENE',
        'description' => 'Cliquez sur l\'image a droite pour afficher les informations sur le bois Thermofrene.',
        'image' => 'thermofrene.jpg',
        'lien' => 'thermofrene.html',
        'alt' => 'Produit 3'
    ),
    array(
        'nom' => 'LE THERMOPIN',
        'description' => 'Cliquez sur l\'image a droite pour afficher les informations sur le bois Thermopin.',
        'image' => 'thermopin.jpg',
        'lien' => 'thermopin.html',
        'alt' => 'Produit 4'
    ),
    array(
        'nom' => 'LE KEBONY',
        'description' => 'Cliquez sur l\'image a droite pour afficher les informations sur le bois Kebony.',
        'image' => 'kebony.jpg',
        'lien' => 'kebony.html',
        'alt' => 'Produit 5'
    )
);
?>
```

2. Renommez `nos_produits.html` en `nos_produits.php`

3. Ajoutez le header PHP en haut du fichier (comme à l'étape 3)

4. Remplacez tous les blocs de produits par une boucle :

```php
<?php include 'produits.php'; ?>

<?php
foreach ($produits as $produit) {
    echo '<div id="produits">';
    echo '<br>' . $produit['nom'] . '<br>';
    echo $produit['description'] . '<br></div>';
    echo '<div id="photoprod">';
    echo '<a href="' . $produit['lien'] . '">';
    echo '<img class="photo" src="' . $produit['image'] . '" alt="' . $produit['alt'] . '" width="300" height="150">';
    echo '</a></div>';
}
?>
```

5. Testez votre page `nos_produits.php`.

---

## Étape 6 : Parcours d'un dossier pour afficher les réalisations

### Objectif

Découvrir comment parcourir un dossier pour afficher dynamiquement toutes les images.

### Instructions

1. Créez un dossier `img/realisations` dans votre répertoire `public_html`

2. Copiez toutes les images de réalisations depuis le répertoire principal vers `img/realisations`. Vous pouvez utiliser les images suivantes (ou toutes celles que vous souhaitez) :
   - Accoya_11.jpg
   - accoya12.jpg
   - accoya_15.jpg
   - accoya_16.jpg
   - garde-corps01.jpg
   - garde-corps03.jpg
   - Pergola 02.jpg
   - Pergola 03.jpg
   - pergolas01.jpg
   - Terrasse accoya -06.jpg
   - Terrasse accoya .jpg
   - Terrasse Accoya08.jpg
   - Terrasse Kebony 01.jpg
   - Terrasse Kebony 04.jpg
   - Terrasse Kebony 05.jpg
   - terrasse00.jpg
   - terrasse01.jpg
   - terrasse02.jpg
   - terrasse04.jpg
   - terrasse05.jpg
   - terrasse06.jpg
   - terrasse07.jpg
   - Thermofrene -09.jpg
   - Thermofrene 03.jpg
   - Thermofrene 05.jpg
   - Thermofrene 06.jpg
   - Thermofrene 07.jpg
   - Thermofrene grisé 02.jpg
   - Thermopin 03.jpg
   - Thermopin 05.jpg
   - Thermopin01.jpg
   - Verda 01.jpg
   - Verda05.jpg
   - Verda07.jpg

3. Renommez `nos_realisations.html` en `nos_realisations.php`

4. Ajoutez le header PHP en haut du fichier

5. Remplacez tous les blocs d'images par le code suivant qui parcourt le dossier :

```php
<?php
$dossier = 'img/realisations';
$fichiers = scandir($dossier);
$compteur = 0;

echo '<div class="realisationphoto">';

foreach ($fichiers as $fichier) {
    // Ignorer les fichiers . et ..
    if ($fichier != '.' && $fichier != '..') {
        // Vérifier que c'est bien une image (extension jpg, jpeg, png, gif)
        $extension = strtolower(pathinfo($fichier, PATHINFO_EXTENSION));
        if (in_array($extension, array('jpg', 'jpeg', 'png', 'gif'))) {
            echo '<img src="' . $dossier . '/' . $fichier . '" alt="" width="200" height="200">';
            $compteur++;
            
            // Créer une nouvelle ligne toutes les 4 images
            if ($compteur % 4 == 0) {
                echo '</div><div class="realisationphoto">';
            }
        }
    }
}

echo '</div>';
?>
```

**Explication du code** :
- `scandir($dossier)` : liste tous les fichiers d'un dossier dans un tableau
- `pathinfo($fichier, PATHINFO_EXTENSION)` : récupère l'extension du fichier
- `in_array()` : vérifie si une valeur existe dans un tableau
- Le modulo `%` permet de créer une nouvelle ligne toutes les 4 images

6. Testez votre page `nos_realisations.php`. Toutes les images du dossier devraient s'afficher automatiquement.

---

## Étape 7 : Traitement d'un formulaire de contact

### Objectif

Créer une page de traitement qui affiche les données soumises par le formulaire.

### Instructions

1. Renommez `contact.html` en `contact.php`

2. Ajoutez le header PHP en haut du fichier

3. Modifiez la balise `<form>` pour qu'elle pointe vers une page de traitement. Remplacez le début du formulaire par :

```php
<form method="POST" action="traitement_contact.php">
```

4. Ajoutez un attribut `name` à chaque champ du formulaire. Voici les modifications à apporter :

```php
<fieldset> 
    <legend>Nom</legend>
    <p><label>Nom</label> <input type="text" name="nom" id="nom" value="" required/></p>
</fieldset>
<fieldset> 
    <legend>Prénom</legend>   
    <p><label>Prénom</label> <input type="text" name="prenom" id="prenom" value="" required/></p>
</fieldset>
<fieldset>
    <legend> CP / Ville </legend>
    <p><label> CP</label> <input type="text" name="code_postal" id="code_postal" value="" maxlength="5" required />
       <label>Ville</label> <input type="text" name="ville" id="ville" value="" required/></p>
</fieldset>
<fieldset>
    <legend>Email</legend>
    <p><label>Email</label> <input type="email" name="email" id="email" value="" required /></p>
</fieldset>
<fieldset> 
    <legend>Tél.</legend>      
    <p><label>N° Tel.</label> <input type="text" name="telephone" id="telephone" value="" maxlength="10" required/></p>
</fieldset>
<fieldset>
    <legend>Messages</legend>
    <textarea name="message" id="message"></textarea>
</fieldset>
```

5. Créez un nouveau fichier `traitement_contact.php` qui affichera les données reçues :

```php
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Confirmation de contact</title>
    <link rel="stylesheet" media="screen" type="text/css" href="site_ste_grad.css"/>
</head>
<body>
    <?php
    $titre_page = "Confirmation";
    include 'header.php';
    ?>
    
    <div style="padding: 20px;">
        <h1>Merci pour votre message</h1>
        <p>Nous avons bien reçu les informations suivantes :</p>
        
        <fieldset>
            <legend>Informations personnelles</legend>
            <p><strong>Nom :</strong> <?php echo $_POST['nom']; ?></p>
            <p><strong>Prénom :</strong> <?php echo $_POST['prenom']; ?></p>
            <p><strong>Code postal :</strong> <?php echo $_POST['code_postal']; ?></p>
            <p><strong>Ville :</strong> <?php echo $_POST['ville']; ?></p>
        </fieldset>
        
        <fieldset>
            <legend>Coordonnées</legend>
            <p><strong>Email :</strong> <?php echo $_POST['email']; ?></p>
            <p><strong>Téléphone :</strong> <?php echo $_POST['telephone']; ?></p>
        </fieldset>
        
        <fieldset>
            <legend>Message</legend>
            <p><?php echo nl2br(htmlspecialchars($_POST['message'])); ?></p>
        </fieldset>
        
        <p><a href="contact.php">Retour au formulaire</a></p>
    </div>
</body>
</html>
```

**Explication** :
- `$_POST` : tableau associatif contenant toutes les données envoyées par le formulaire via la méthode POST
- `htmlspecialchars()` : convertit les caractères spéciaux en entités HTML pour éviter les problèmes de sécurité
- `nl2br()` : convertit les retours à la ligne en balises `<br>`

6. Testez votre formulaire en remplissant tous les champs et en cliquant sur "Send Message". Vous devriez voir s'afficher une page de confirmation avec toutes vos données.

---

## Étape 8 : Création de la base de données

### Objectif

Créer une base de données MySQL/MariaDB pour stocker les messages de contact.

### Instructions

1. Connectez-vous à MySQL en ligne de commande avec la commande suivante :

```bash
mysql -u mysql -p
```

Entrez le mot de passe quand il vous est demandé.

2. Créez une nouvelle base de données nommée `vitrine_grad` :

```sql
CREATE DATABASE vitrine_grad CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. Sélectionnez cette base de données :

```sql
USE vitrine_grad;
```

4. Créez une table `messages` avec la structure suivante :

```sql
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(30) NOT NULL,
    prenom VARCHAR(30) NOT NULL,
    code_postal VARCHAR(5) NOT NULL,
    ville VARCHAR(30) NOT NULL,
    email VARCHAR(255) NOT NULL,
    telephone VARCHAR(10) NOT NULL,
    message TEXT NOT NULL,
    date_creation DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Explication de la structure** :
- `id` : identifiant unique auto-incrémenté (clé primaire)
- `nom`, `prenom`, `code_postal`, `ville`, `email`, `telephone` : champs texte pour les informations du formulaire
- `message` : champ texte pour le message (peut être long)
- `date_creation` : date et heure de création du message (remplie automatiquement)

5. Vérifiez que la table a bien été créée :

```sql
SHOW TABLES;
DESCRIBE messages;
```

---

## Étape 9 : Connexion à la base de données avec PDO

### Objectif

Apprendre à se connecter à une base de données MySQL avec PDO (PHP Data Objects).

### Instructions

1. Créez un fichier `config.php` qui contiendra les paramètres de connexion à la base de données :

```php
<?php
// Paramètres de connexion à la base de données
$db_host = 'localhost';
$db_name = 'vitrine_grad';
$db_user = 'mysql';
$db_pass = 'mysql';

// Connexion à la base de données avec PDO
try {
    $pdo = new PDO("mysql:host=$db_host;dbname=$db_name;charset=utf8mb4", $db_user, $db_pass);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
} catch(PDOException $e) {
    die("Erreur de connexion à la base de données : " . $e->getMessage());
}
?>
```

**Explication** :
- `PDO` : classe PHP pour se connecter à une base de données de manière sécurisée
- `try...catch` : gestion des erreurs. Si la connexion échoue, un message d'erreur s'affiche
- `setAttribute()` : configure le comportement de PDO (affichage des erreurs, format de récupération des données)

2. Testez votre connexion en créant un fichier `test_connexion.php` :

```php
<?php
include 'config.php';
echo "Connexion à la base de données réussie !";
?>
```

Si vous voyez le message "Connexion à la base de données réussie !", votre connexion fonctionne correctement.

---

## Étape 10 : Enregistrement des messages dans la base de données

### Objectif

Modifier la page de traitement du formulaire pour enregistrer les données dans la base de données.

### Instructions

1. Modifiez le fichier `traitement_contact.php` pour inclure la connexion à la base de données et insérer les données :

```php
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Confirmation de contact</title>
    <link rel="stylesheet" media="screen" type="text/css" href="site_ste_grad.css"/>
</head>
<body>
    <?php
    $titre_page = "Confirmation";
    include 'header.php';
    include 'config.php';
    
    // Récupération des données du formulaire
    $nom = $_POST['nom'];
    $prenom = $_POST['prenom'];
    $code_postal = $_POST['code_postal'];
    $ville = $_POST['ville'];
    $email = $_POST['email'];
    $telephone = $_POST['telephone'];
    $message = $_POST['message'];
    
    // Préparation de la requête SQL d'insertion
    $sql = "INSERT INTO messages (nom, prenom, code_postal, ville, email, telephone, message) 
            VALUES ('$nom', '$prenom', '$code_postal', '$ville', '$email', '$telephone', '$message')";
    
    // Exécution de la requête
    try {
        $pdo->exec($sql);
        $succes = true;
    } catch(PDOException $e) {
        $succes = false;
        $erreur = $e->getMessage();
    }
    ?>
    
    <div style="padding: 20px;">
        <?php if ($succes): ?>
            <h1>Merci pour votre message</h1>
            <p>Votre message a bien été enregistré dans notre base de données.</p>
        <?php else: ?>
            <h1>Erreur</h1>
            <p>Une erreur s'est produite lors de l'enregistrement : <?php echo $erreur; ?></p>
        <?php endif; ?>
        
        <fieldset>
            <legend>Informations personnelles</legend>
            <p><strong>Nom :</strong> <?php echo htmlspecialchars($nom); ?></p>
            <p><strong>Prénom :</strong> <?php echo htmlspecialchars($prenom); ?></p>
            <p><strong>Code postal :</strong> <?php echo htmlspecialchars($code_postal); ?></p>
            <p><strong>Ville :</strong> <?php echo htmlspecialchars($ville); ?></p>
        </fieldset>
        
        <fieldset>
            <legend>Coordonnées</legend>
            <p><strong>Email :</strong> <?php echo htmlspecialchars($email); ?></p>
            <p><strong>Téléphone :</strong> <?php echo htmlspecialchars($telephone); ?></p>
        </fieldset>
        
        <fieldset>
            <legend>Message</legend>
            <p><?php echo nl2br(htmlspecialchars($message)); ?></p>
        </fieldset>
        
        <p><a href="contact.php">Retour au formulaire</a></p>
    </div>
</body>
</html>
```

**Explication** :
- `$pdo->exec($sql)` : exécute une requête SQL qui ne retourne pas de résultats (comme INSERT, UPDATE, DELETE)
- La requête SQL `INSERT INTO` ajoute une nouvelle ligne dans la table `messages`
- Les valeurs sont directement insérées dans la requête (nous verrons les requêtes préparées dans un cours ultérieur pour plus de sécurité)

2. Testez votre formulaire en remplissant tous les champs. Après soumission, vérifiez dans votre base de données que le message a bien été enregistré :

```sql
SELECT * FROM messages;
```

Vous devriez voir apparaître votre message dans la table.

---

## Note sur l'utilisation d'Adminer

Toutes les opérations sur la base de données effectuées dans ce TP peuvent également être réalisées via l'interface web Adminer qui est déjà installée sur votre environnement. Vous avez d'ailleurs déjà utilisé cette interface dans des travaux précédents.

Pour la suite de votre apprentissage, nous vous conseillons d'utiliser Adminer pour :
- Vérifier la structure de vos tables
- Consulter les données enregistrées
- Tester vos requêtes SQL
- Visualiser facilement les résultats de vos insertions

L'interface graphique d'Adminer facilite la compréhension de la structure de votre base de données et permet de vérifier rapidement que vos requêtes PHP fonctionnent correctement.

