# 📖 Solve - Normes de Codage

---

### 🧾 Informations du projet

Chaque projet ou ressource doit contenir en tête de son README.md :

```markdown
# Nom de la ressource

📌 Auteur principal : Prénom et ou pseudo  
👥 Auteurs secondaires : Liste des contributeurs ayant modifié le code  
📅 Date de la dernière modification : JJ/MM/AAAA  
🗂️ Type de projet : FiveM, Web, Discord, Backend, etc.  
📃 Description : Brève description de l'objectif du script ou module  
```

### 🌍 Langue et style

- **Variables/fonctions/classes :** anglais
- **Commentaires :** français
- **Fichiers :** kebab-case ou snake_case selon le langage

### 🌐 Git & branches

- **main :** branche stable (production)
- **dev :** branche de développement
- **Optionnel :** feature/, fix/, docs/

### 💬 Commentaires

- Toujours en français
- Utiliser des emojis/tags pour signaler les zones importantes

**Lua :**
```lua
-- 🔁 Recharge l'inventaire du joueur
function reloadInventory(playerId)
    -- TODO : Ajouter vérification du poids
end
```

**JavaScript :**
```javascript
// 🔒 Vérifie si l'utilisateur est admin
if (!isAdmin(user)) return
```

### 🚀 Commits Git

- **feat:** ajout de fonctionnalité
- **fix:** correction
- **refactor, docs, chore**

**Exemple :**
```bash
git commit -m "feat(inventory): add drag and drop support"
```

### 🛡️ Sécurité et bonnes pratiques

- Ne pas exposer d'infos sensibles
- Valider les données côté serveur
- Pas de console.log/print en prod
- Découper les fonctions longues
- Centraliser les helpers dans /utils

---

## 🎯 Standards de codage

### Nommage des variables

Règles concernant notre système de nommage personnalisé

À chaque fois que vous devez créer ou utiliser une variable, vous devez respecter ces normes.

#### Choix des mots

✔️ Choisissez des mots anglais lisibles (HorizontalAlignment est mieux que AlignmentHorizontal)  
✔️ Privilégiez la lisibilité à la brièveté (CanScrollHorizontally est mieux que ScrollableX)  
❌ N'utilisez aucun caractère spécial ou non-alphanumérique  
❌ N'utilisez pas de mot-clé déjà existant (GetLength est mieux que GetInt)  
❌ N'utilisez pas d'abréviations ou de contractions (CreateWindow plutôt que CreateWin)  
❌ N'utilisez pas d'acronymes qui ne sont pas largement acceptés (API est correct, AEAP ne l'est pas)  

#### Préfixe de type

Ces normes sont inspirées du "Système de Notation Hongroise", utilisé par Microsoft pour rendre leur code plus compréhensible.
Vous devez mettre un préfixe avant le nom d'une variable selon son type.

**Pour Lua (FiveM) :**
```lua
i       integer/number                      iMoney = pOwner.PlayerData.money.cash
b       boolean                             bDead = pOwner.PlayerData.metadata.isdead
s       string                              sReason = "Vous n'êtes pas autorisé à faire cela."
t       table                               tOffences = {"RDM", "VDM"}

c       color                               cBackground = {r = 123, g = 231, b = 132}
p       player                              pOwner = QBCore.Functions.GetPlayer(source)
e       entity                              eVehicle = GetVehiclePedIsIn(ped, false)
v       vgui/ui element                     vFrame = document.getElementById("mainFrame")
o       object (non listé ci-dessus)        oCoords = GetEntityCoords(ped)

vec     vector                              vecPlayerPos = GetEntityCoords(pOwner.PlayerData.source)

by      byte                                byH = string.byte('H')
nil     nil                                 nilUseless = nil
fc      function                            fcCallback = function() print("Bonjour monde!") end
```

**Pour JavaScript/Web :**
```javascript
i       integer/number                      let iMoney = player.money.cash;
b       boolean                             let bIsOnline = player.online;
s       string                              let sMessage = "You are not authorized";
a       array                               let aPlayers = QBCore.Functions.GetPlayers();
o       object                              let oPlayerData = player.PlayerData;

e       element (DOM)                       let eButton = document.getElementById("submit");
fc      function                            let fcCallback = () => console.log("Hello!");
```

#### Nom des fonctions

**✔️ Façon correcte (Lua)**

```lua
local t = {}
t.fcCallback = function(s) print(s) end

function t:Print(s)
    print("Bonne façon! :D", s)
end
```

**✔️ Façon correcte (JavaScript)**

```javascript
const t = {};
t.fcCallback = (s) => console.log(s);

t.Print = function(s) {
    console.log("Bonne façon! :D", s);
};
```

#### Identifiants des événements FiveM

Lors de l'utilisation d'événements FiveM, vous devez  spécifier des identifiants uniques.
Format spécifique : `S:Addon:EventName`. L'objectif ne doit pas contenir plus de 2 mots.

**Exemples :**

```lua
✔️ RegisterNetEvent("S:Banking:TransferMoney")
✔️ RegisterNetEvent("S:Fuel:ConsumeGas")
✔️ RegisterNetEvent("S:Inventory:UpdateItems")
✔️ TriggerEvent("S:HUD:RefreshDisplay")
```

#### Identifiants des timers

Format spécifique : `S:Addon:Goal`. L'objectif ne doit pas contenir plus de 2 mots.

**Exemples Lua (FiveM) :**

```lua
✔️ SetTimeout(5000, function() end) -- Nommé: "S:Banking:UpdateBalance"
✔️ CreateThread(function() end) -- Nommé: "S:Fuel:ConsumeGas"
```

**Exemples JavaScript :**

```javascript
✔️ setTimeout(fcCallback, 5000); // S:Banking:UpdateBalance
✔️ setInterval(fcCallback, 30000); // S:Weather:UpdateSystem
```

#### Casse

Pour les noms de fonctions, utilisez CamelCase avec la première lettre en majuscule.

```lua
✔️ function GetMoney(pUser)   
✔️ function QBCore:GetMoney(pUser)  
❌ function getMoney(pUser)  
```

```javascript
✔️ function GetMoney(pUser)
✔️ QBCore.GetMoney = function(pUser)
❌ function getMoney(pUser)
```

Pour les noms de variables, utilisez CamelCase avec la première lettre en minuscule (le préfixe de type comme vu précédemment).

---

## 🎯 Normes générales

#### Fonctions dépréciées

N'utilisez aucune fonction/événement déclarée comme "**dépréciée**" sur la documentation officielle FiveM ou QBCore.

#### Préférer les appels orientés objet

**Lua :**
```lua
local sEx = "Salut les gars !"
sEx:sub(2, 5)
sEx:find("gars")
```

**JavaScript :**
```javascript
let sEx = "Salut les gars !";
sEx.substring(2, 5);
sEx.indexOf("gars");
```
