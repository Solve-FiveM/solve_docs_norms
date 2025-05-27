# 📖 Solve - Normes de Codage

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
Vous devez mettre un préfixe avant le nom d'une variable selon son type. Vous pouvez voir la liste complète ci-dessous (avec exemples).

```lua
i       integer/number                      iMoney = pOwner:GetMoney()
b       boolean                             bDead = pOwner:IsDead()
s       string                              sReason = "Vous n'êtes pas autorisé à faire cela."
t       table                               tOffences = {"Free-kill", "Free-arrest"}

c       color                               cBackground = Color(123, 231, 132)
p       player                              pOwner = player.GetAll()[1]
e       entity                              eVehicle = Entity(11)
v       vgui                                vBase = vgui.Create("DFrame")
m       vmatrix                             mText = Matrix()
o       object (non listé ci-dessus)        oPlane = solve.CreatePlane()

vec     vector                              vecPlayerPos = pOwner:GetPos()
ang     angle                               angShootingAt = pOwner:GetAngles()

by      byte                                byH = string.byte('H')
nil     nil                                 nilUseless = nil
fc      function                            fcCallback = function() print("Bonjour monde!") end
th      thread                              thSQLWait = coroutine.create(function() print("Je suis dans une routine!") end)
```

Dans certains cas, les MetaTables peuvent être en majuscules complètes : `local PLAYER = FindMetaTable("Player")`.

#### Nom des fonctions

Vous pouvez voir dans la liste ci-dessus qu'il y a un champ "function".
C'est parce qu'initialiser une fonction et stocker une fonction sont 2 choses différentes.

**✔️ Façon correcte**

```lua
local t = {}
t.fcCallback = function(s) print(s) end

function t:Print(s)
    print("Bonne façon! :D", s)
end
```

**❌ Façon incorrecte**

```lua
local t = {}
t.callback = function(s) print(s) end

function t:fcPrint(s)
    print("Mauvaise façon! D:", s)
end
```

#### Identifiants des hooks

Lors de l'utilisation de hooks, vous devez spécifier des identifiants uniques.
Pour être plus clair entre chaque développeur du projet, nous avons défini un format spécifique : `S:Addon:HookName`. L'objectif ne doit pas contenir plus de 2 mots.

**Exemples :**

```lua
✔️ hook.Add("PlayerSay", "S:Mining:PlayerSay", function() end)  
✔️ hook.Add("SetupMove", "S:Security:SetupMove", function() end)  
✔️ hook.Add("PlayerSpawn", "S:Banking:PlayerSpawn", function() end)
```

#### Identifiants des timers

Lors de l'utilisation de timers, vous devez spécifier des identifiants uniques.
Pour être plus clair entre chaque développeur du projet, nous avons défini un format spécifique : `S:Addon:Goal`. L'objectif ne doit pas contenir plus de 2 mots.

**Exemples :**

```lua
✔️ timer.Create("S:Queue:WaitConnect", 5, 0, fcCallback)
✔️ timer.Create("S:Banking:UpdateBalance", 30, 0, fcCallback)
✔️ timer.Create("S:Fuel:ConsumeGas", 10, 0, fcCallback)
```

#### Identifiants de réseau

Lors de l'utilisation des nets, vous devez spécifier des identifiants uniques.
Comme pour les hooks, nous devons être plus clairs entre chaque développeur du projet, donc nous avons défini un format spécifique : `S:Addon:Goal`. L'objectif ne doit pas contenir plus de 2 mots.

**Exemples :**

```lua
✔️ util.AddNetworkString("S:Mining:SellOre")  
✔️ util.AddNetworkString("S:Security:WarnPlayer")  
✔️ util.AddNetworkString("S:Banking:TransferMoney")
✔️ util.AddNetworkString("S:Inventory:UpdateItems")
```

#### Casse

Pour les noms de fonctions, utilisez CamelCase avec la première lettre en majuscule.

```lua
✔️ function GetMoney(pUser)   
✔️ function Solve:GetMoney(pUser)  
❌ function getMoney(pUser)  
❌ function Solve:getMoney(pUser)  
```

Pour les noms de variables, utilisez CamelCase avec la première lettre en minuscule (le préfixe de type comme vu précédemment).

```lua
✔️ local iMoney = GetMoney(pUser)  
❌ local IMoney = GetMoney(pUser)  
❌ local I_MONEY = GetMoney(pUser)  
```

---

## 🎯 Normes générales

Normes générales que vous devrez suivre pendant vos sessions.

Ces sont les normes générales que vous devez suivre de toute façon.

#### Fonctions dépréciées

N'utilisez aucune fonction/hook déclarée comme "**dépréciée**" sur le wiki officiel. À la place, utilisez les fonctions recommandées liées au message d'avertissement.

#### Préférer les appels orientés objet

Par "*appels orientés objet*", je veux dire : Essayez d'utiliser ces appels

```lua
local sEx = "Salut les gars !"
sEx:sub(2, 5)
sEx:find("gars")
```

au lieu de ceux-ci

```lua
local sEx = "Salut les gars !"
string.sub(sEx, 2, 5)
string.find(sEx, "gars")
```

**Attention :** Utiliser les appels par défaut n'est pas interdit. Essayez simplement de faire de votre mieux pour utiliser les premiers.

#### Formatage des chaînes

Au lieu d'utiliser la concaténation *(non protégée contre les injections)*, nous pouvons utiliser la fonction **string.format**. Dès que vous le pouvez, veuillez l'utiliser.

**Exemples :**

```lua
✔️ ("Bonjour %s !"):format(sNick)
✔️ string.format("Bonjour %s !", sNick)
❌ "Bonjour "..sNick.." !"
```

#### Guillemets

Vous avez 2 types de guillemets : 'guillemets-simples', "guillemets-doubles". Vous devez savoir quand vous voulez utiliser ceux-ci :
* Utilisez "guillemets-doubles" à chaque fois, sauf si :
  * Il n'y a qu'un seul caractère

**Exemples :**

```lua
✔️ print("bonjour monde!")  
✔️ print('b', 'o', 'n', 'j', 'o', 'u', 'r')  
❌ print('bonjour monde!')  
❌ print("b")
```

#### Longueur

Nous avons plusieurs façons d'obtenir la longueur de certaines variables (string, table). Nous utiliserons la même méthode à chaque fois.

**Taille des tables**

```lua
✔️ #tbl
❌ table.Count(tbl) -- Uniquement quand les clés sont non-séquentielles ou non-numériques.
```

**Taille des chaînes**

```lua
✔️ #str
❌ string.len(str)
```

#### Commentaires

Vous devez expliquer à chaque développeur qui lira votre code comment il fonctionne. Donc, **vous devez décrire l'utilité de chaque fonction** que vous créez (en une seule phrase).

```lua
-- Trouve un objet joueur par son nom
function Solve.Admin:GetPlayerByName(sName)
    return player.GetAll()[1]
end
```

⚠️ Vous **devez** utiliser `--` pour faire des **commentaires simples** et

```lua
--[[
Pour faire
de plus gros commentaires
--]]
```

---

## 🎯 Normes conditionnelles

#### Usage

Nous savons tous à quel point il est important de vérifier nos valeurs à un moment donné. Cependant, nous vous demandons d'**utiliser le gestionnaire d'erreur Lua au lieu d'utiliser des conditions inutiles**.

En effet, imaginons que vous fassiez une fonction pour compter le nombre de caractères alphanumériques d'une chaîne. Si un autre développeur utilise votre fonction et met une table au lieu d'une chaîne, voici ce qui se passe :

```lua
-- Une fonction pour compter le nombre de caractère(s) alphanumérique(s) dans une chaîne
local function CountAlphanumerics(sText, bUseCondition)

    if bUseCondition and not isstring(sText) then return end -- Voici la condition dont nous parlons

    local i = 0
    for s in string.gmatch(sText, "[a-zA-Z0-9]") do
        i = i + 1
    end

    return i

end

local sTest = "Bonjour monde"

-- ❌ Résultat avec la condition (débogage chronophage)
print(CountAlphanumerics(sTset, true)) -- AUCUNE SORTIE - Nous ne savons pas quel est le problème jusqu'à ce que nous remarquions la faute de frappe

-- ✔️ Résultat sans la condition (beaucoup plus facile à déboguer)
print(CountAlphanumerics(sTset, false)) -- SORTIE D'ERREUR - Nous avons immédiatement un tas d'informations du gestionnaire d'erreur Lua
```

⚠️ **ATTENTION :** Les conditions sont toujours obligatoires dans certains cas. Soyez intelligent. Vous êtes responsable de toute condition manquante qui conduit à un problème de sécurité.

#### Parenthèses

Vous ne pouvez utiliser des parenthèses **que lorsque c'est nécessaire**. Sinon, Lua fait le travail pour nous.

```lua
✔️ if 1 + 1 == 2 then  
✔️ if (2 + 2) * 2 == 8 then  
✔️ if 2 + 2 * 2 + 2 / 2 == 7 then  
❌ if (1 + 1) == 2 then  
❌ if (1 + 1 == 2) then
```

#### Symboles

Utilisez uniquement les symboles et opérateurs lua natifs dans les conditions. Voici ce que vous êtes autorisé ou non à faire :

```lua
✔️ if 1 + 1 ~= 3 then
❌ if 1 + 1 != 3 then

✔️ if not (1 + 1 == 3) then -- ne faites pas cela, c'est juste un exemple.
❌ if !(1 + 1 == 3) then
```

#### Inverse

N'utilisez pas de parenthèses lors de l'utilisation de mots-clés inverses ("**not**", "**~**"). Voici ce que vous êtes autorisé ou non à faire :

```lua
❌ if not (IsValid(pPly) and pPly:IsPlayer()) then return end
✔️ if not IsValid(pPly) or not pPly:IsPlayer() then return end
```

---

## 🎯 Normes d'espacement

Les normes d'espacement incluent les normes d'indentation et les normes d'espaces blancs/sauts de ligne. Ce sont la partie la plus importante des standards de codage et la plus importante.

#### Lors de l'utilisation d'une fonction, supprimez les espaces avant et après les arguments s'ils existent.

**❌ Incorrect**

```lua
function log( sMsg, bError )

   if bError then
      Error( sMsg )
   else
      print( sMsg )
   end

end
```

**✔️ Correct**

```lua
function log(sMsg, bError)

   if bError then
      Error(sMsg)
   else
      print(sMsg)
   end

end
```

#### Lors de la création d'une fonction ou d'une condition, mettez des espaces sur la première et la dernière ligne.

**ATTENTION :** Cela ne s'applique pas lorsque le contenu prend quelques lignes (<= 3). **NOTE :** Les boucles sont considérées comme des fonctions dans ce cas.

**❌ Incorrect**

```lua
function lol()
   print("ouiouibaguette")
   print("nonnonnbaguette")
end
```

**✔️ Correct**

```lua
function lmao()

   if 1 + 1 == 2 then
      print("ouinonbaguette")
   end

end

function lol()
   print("ouiouibaguette")
   print("nonnonbaguette")
end

function test()
   print("ouiouibaguette")
end
```

#### Avoir moins de 80 colonnes

**❌ Incorrect**

```lua
if not IsValid(pKiller) or not isnumber(iDamage) or not isstring(sKillType) then return end
```

**✔️ Correct**

```lua
if not IsValid(pKiller) then return end
if not isnumber(iDamage) or not isstring(sKillType) then return end
```

#### Faire un saut de ligne après un bloc de déclaration de variable

**✔️ Correct**

```lua
function hi()
   
   local sFirst = "salut"
   local sSecond = "les copains"
   local sSeparator = " "

   print(sFirst..sSeparator..sSecond)

end
```

#### N'utilisez pas d'espaces pour la concaténation

```lua
✔️ print("Salut comment vas-tu, "..LocalPlayer():Nick().." ?")  
❌ print("Salut comment vas-tu, " .. LocalPlayer():Nick() .. " ?")  
❌ print("Salut comment vas-tu, " ..LocalPlayer():Nick().. " ?")  
```

#### Utilisez des espaces lors de l'écriture d'informations dans un net

**❌ Incorrect**

```lua
net.Start("name")
net.WriteString("Ceci est un net non-indenté !")
net.WriteUInt(8, 4)
net.SendToServer()
```

**✔️ Correct**

```lua
net.Start("name")
   net.WriteString("Ceci est un net indenté !")
   net.WriteUInt(8, 4)
net.SendToServer()
```

---

## 🎯 Exemples spécifiques Solve

Aucun exemple pour le moment...

---

*Dernière mise à jour : [27/05/2025]*  
*Alimenté par Solve Core & Qbox Core*
