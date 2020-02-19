* Exercice 1. Variables d’environnement*  
*1.Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?*  
**Pour trouver les chemins des dossiers bash des commandes tapées par l'utilisateur on tape : printetv PATH et ca nous renvois tout ces chemins /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin**  
*2.Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dansvotre répertoire personnel?*  
**C'est la variable environnement $HOME, pour le vérifier on tape printenv HOME on voit la chemin de cd**  
*3.Explicitez le rôle des variables LANG,PWD,OLDPWD,SHELL et_*  
**LANG : Pour nous donner la langue qu'utilise les logiciels pour communiquer avec l'utilisateur  
PWD : Elle contient le chemin du repertoire courant  
OLDPWD :  Elle contient le  chemin de la derniere commande cd**  
SHELL : Elle contient le chemin /bin/bash  qui est un programme qui permet d'interpreter les commandes
_ : Elle contient le chemin vers la commande printenv :  contains directory before the last cd command**  
*4.Créez une variable locale MY_VAR(le contenu n’a pas d’importance). Vérifiez que la variable existe.*  
**je créer la variable : MYVAR="abcd" ensuite je verifie avec echo $MYVAR et je vois bien le contenu 'abcd'**
*5.Tapez ensuite la commande bash. Que fait-elle? La variable MY_VAR existe-t-elle? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.*  
**Elle creer une nouvelle instance du bash non elle ,n'existe pas car elle est locale,il faut que ca soit une variable environnement pour la voir sur les bash**   
*6.Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.*  
**export MY_VAR="abcd" et ensuite je fais bash et echo $MY_VAR,et je vois bien ma variable**   
*7.Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Aﬀicher la valeur de NOMS pour vérifier que l’affectation est correcte*  
**export NOMS="ZAK AYOUB" et echo $NOMS ca affiche ZAK AYOUB**  
*8.Ecrivez une commande qui aﬀiche ”Bonjour à vous deux, binôme1 binôme2!” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.*  
**echo "Bonjour à vous deux,"$NOMS "!"**  
*9.Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset?*  
**La commande unset supprime la variable, donc elle n'existe plus. Si on donne la valeur vide à une variable, bien qu'elle ne contient rien elle existe toujours** 
*10.Utilisez la commande echo pour écrire exactement la phrase :$HOME =chemin(où chemin est votredossier personnel d’après bash)*  
**echo '$HOME :' $HOME**  
  
    
*Exercice 2. Contrôle de mot de passe*  
*Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non aucontenu d’une variablePASSWORDdont le contenu est codé en dur dans le script. Le mot de passe saisi parl’utilisateur ne doit pas s’aﬀicher.*
**#!/bin/bash
PASSWORD=admin
read -p "Saisissez le mot de passe" -s mdp
echo 
if [ $PASSWORD = $mdp ]
then
        echo "GOOD"
else
        echo "WRONG"

fi**  
  
*Exercice 3. Expressions rationnelles  
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètreest un nombre réel :
function is_number()  
{re='^[+-]?[0-9]+([.][0-9]+)?$'  
if ! [[ $1 =~ $re ]] ;   
then 
return 1  
else  
return 0  
fi}  
Il aﬀichera un message d’erreur dans le cas contraire.*  
**#!/bin/bash  
function is_number(){  #on recupere la fonction donné
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ;
 then return 1 # elle retourne 1 quand ce n'est pas un nombre
else
return 0 # et retourne 0 quand c'est un nombre
fi }
read -p "entrez un nombre  :  " nbr  #on rentre la reponse de l'user dans nbr
echo
is_number $nbr #on execute la fonction avec nbr
if [ $? = 0 ]  #avec $? on recupere ce que renvoi la derniere fonction
then
echo "c'est un nombre"
else
echo "ce n'es pas un nombre"
fi**  
  
*Exercice 4. Contrôle d’utilisateur  
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il aﬀiche le message : ”Utilisation :nom_du_scriptnom_utilisateur”,où nom_du_scriptest le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement)* 
**
#!/bin/bash

if [ -z $1 ];then
        echo "Utilisation : $0 nom_utilisateur"
else
        for user in $(cut -d: -f1 /etc/passwd)
        do
                if [ $user = $1 ];then
                        echo "Utilisateur existant :)"
                        exit
                fi
        done
        echo "Utilisateur inexistant"
fi**

*Exercice 5. Factorielle  
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera quel’utilisateur saisit toujours un entier naturel).*  







