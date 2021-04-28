# Connect-System

Je vous montre comment faire un system de connexion simple et facile à utiliser, il ne vous manque plus qu'a l'adapter a vos project. 

------------------------------------Création Du Compte------------------------------------

Pour commancer vous devez créer une classe qui va contenir toute les information comme si-dessous : 
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Json
{
    class VotreClasse
    {
        public string mail { get; set; }
        public string id { get; set; }
        public string pass { get; set; }
        public bool autoReconnect { get; set; }
        public DateTime date { get; set; }

    }
}
```

Après avoir créer la classe, on va attribuer pour chaque variable de `VotreClasse` des données dans la classe `Program`, tous ca rangé dans une méthode (avec en argumment les varible de `VotreClasse` :
```cs
            VotreClasse votreClasse = new VotreClasse
            {
                mail = "mailPersonne@exxemple.com",
                id = "peronne35",
                pass = "motDePasse",
                autoReconnect = false,
                date = DateTime.Now
            };
```

Ensuite on va créer le fichier `.json` qui va contenir l'object `VotreClasse`. Pour cela n'oublier pas d'utiliser le `using System.IO;` ainsi que `using Newtonsoft.Json;`.
```cs
            string json = JsonConvert.SerializeObject(votreClasse);

            using (StreamWriter sw = new StreamWriter("fileName.json"))
            {
                sw.WriteLine(json);
                sw.Close();
            }
```
Pour finir la méthode de Création du compte, on va vérifier que notre fichier a bien été créer.
```cs
            if (File.Exists("fileName.json"))
                return true;
            else
                return false;
```
Vous devez avoir ce résultat : 
```cs
        public static bool CreateAccount(string mail, string id, string pass, bool autoReconnect)
        {
            VotreClasse votreClasse = new VotreClasse
            {
                mail = "mailPersonne@exxemple.com",
                id = "peronne35",
                pass = "motDePasse",
                autoReconnect = false,
                date = DateTime.Now
            };

            string json = JsonConvert.SerializeObject(votreClasse);

            using (StreamWriter sw = new StreamWriter("fileName.json"))
            {
                sw.WriteLine(json);
                sw.Close();
            }

            if (File.Exists("fileName.json"))
                return true;
            else
                return false;
        }
```

------------------------------------Connexion------------------------------------

Pour que l'utilisateur puisse se connecter nous allons commancer par deserializer notre fichier `.json` à l'aide d'un `StreamReader` et de `JsonConvert`
```cs
            string json;
            using(StreamReader sr = new StreamReader("fileName.json"))
            {
                json = sr.ReadToEnd();
                sr.Close();
            }
```

Ensuite nous allons le deserializer : 
```cs
VotreClasse votreClasse = JsonConvert.DeserializeObject<VotreClasse>(json);
```

Puis pour finir cette méthode on va vérifier que l'utilisateur a entrer les bons identifiants : 
```cs
            if(votreClasse.id == id)
            {
                if(votreClasse.pass == pass)
                {
                    Console.WriteLine("Vous etes connecter");
                    return true;
                }
                else
                {
                    Console.WriteLine("Mot de passe Incorrect");
                    return false;
                }
            }
            else
            {
                Console.WriteLine("Identifiant Incorrect");
                return false;
            }
```
Vous devez avoir ce résultat : 
```cs
public static bool Login(string id, string pass)
        {
            string json;
            using(StreamReader sr = new StreamReader("fileName.json"))
            {
                json = sr.ReadToEnd();
                sr.Close();
            }

            VotreClasse votreClasse = JsonConvert.DeserializeObject<VotreClasse>(json);

            if(votreClasse.id == id)
            {
                if(votreClasse.pass == pass)
                {
                    Console.WriteLine("Vous etes connecter");
                    return true;
                }
                else
                {
                    Console.WriteLine("Mot de passe Incorrect");
                    return false;
                }
            }
            else
            {
                Console.WriteLine("Identifiant Incorrect");
                return false;
            }
        }
```
