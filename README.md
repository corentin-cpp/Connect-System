# Connect-System

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
------------------------------------Création Du Compte------------------------------------

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
Pour finir la méthode de Création du compte on va vérifier que notre fichier a bien été créer.
```cs
            if (File.Exists("fileName.json"))
                return true;
            else
                return false;
```
