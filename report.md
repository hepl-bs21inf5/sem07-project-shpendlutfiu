# projet Shpend Lutfiu

# journal de bord :

## semaine 1

### Temps passé

 Tâche, Temps passé, Commentaire :

- vue.js, 1h30, bug lorsque je voulais faire le npm

- bootstrap, 30 min

- quiz, 1h30

- Total : 3h30

### questions

main.ts: c'est le fichier qui gert tous les autres fichier et qui les gèrent. par exemple, il importe boostrap, vue et importe le langage javascript pour qu'on puisse l'utiliser dans nos fichier.

main.css: il sert à gérer les styles de notre page web.

App.vue: il gère notre navebar avec ces icons et sa constitution.

router/index.ts: c'est ce qui permet de créer le site web sur le navigateur.

AboutView.vue: pour faire l'onglet "à propos".

HomeView.vue: pour avoir les titres, sous titres et paragraphe du quiz.

QuizForm.vue: fichier qui sert à faire le quiz et ses questions.

Dans le fichier QuizForm.vue :
Quelles sont les similarités et les différences entre ref et computed ?
-similarités: elle permette toute les deux de gérer des variables, elles sont toutes les deux utilisé dans vue.
-différences : computed ne peut être changé directement alors que ref oui, computed est une valeur calculé alors que ref est une variable qui peut définit directement.

Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?
-il affiche une nouvelle fenêtre pour nous indiquer nos points et nos bonnes réponses.

Qu'est-ce qu'un v-model ?
-il permet de choisir une réponse pour une question, il permet de poser une question et va stocker la réponse.

À quoi sert le :class="{ disabled: !filled }" ?
-il sert à pouvoir appuier sur le bonton terminer quand tout les questions sont répondue.

## semaine 2

### Temps passé

Tâche, Temps passé, Commentaire :
-questionradio, 1h, pas de commentaire

-questiontext, 45min, difficulté à trouver quoi changer pour que ça marche

-API, 1h, difficulté à trouver dans quel fichier il fallait faire les changements

total: 2h45min

### questions

Quelle est la différence entre un prop et un modèle (v-model) ?

-le v-model sychronise l'information dans les deux côtés alors que prop fait uniquement dans un seul sens.

Comment rendre la propriété placeholder optionnelle ?

- on fait un placeholder par défaut quand il n'y en a pas dans notre modele.

## semaine 3

### Temps passé

Tâche, Temps passé, Commentaire :

réponse, 30min, pas de difficulté
score, 20min, pas de difficulté
total: 50min

#### questions

À quoi sert l'option immediate: true dans le watch ? Que se passe-t-il si on l'enlève ou si on met immediate: false ?

- pour qu'on aille une valeur de départ avan que l'ordinateur execute le code. si on ne met pas cela, l'ordinateur ne va pas mettre de valeur tant que nous n'avons pas fait de changement dans la réponse mise sur la question sur le site.

Proposer une autre manière de calculer le score (réécrire la fonction du computed) et comparer les deux méthodes.

- faire deux nouvelles variables score et scoretotale, les incrémentés pour chaque question, pour le score uniquement lorsque la réponse mise est juste et l'autre à chaque question. nous n'allons pas avoir le score en temps réel mais uniquement lorsque nous aurons appuyer sur le bontons.

## semaine 4

### Temps passé

Tâche, Temps passé et Commentaire :

état, 30min, faire attention au nom des variables + faire attention aux questiontext car quand on écrit et qu'on efface, cela ne compte pas comme null et du coup compte comme un filled

boutons, 20min, pas de difficulté

réponse immuable, 5min, pas de difficulté

### questions

Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else) ?

model.value =
value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;

- if (value.value === props.answer){
  model.value = QuestionState.Correct;
  }else{model.value = QuestionState.Wrong;
  }

Comment pourrait-on réécrire autrement la logique du watch sur value ?

- watch(
  value,
  (newValue) => {
      model.value = newValue === null ? QuestionState.Empty : QuestionState.Fill;
  },
  { immediate: true },
)
celui-ci est pour le QuestionRadio.vue. Pour QuestionText.vue, il faut remplacer le null par "".

## semaine 5

### Temps passé

Tâche, Temps passé, Commentaire :

- réponse détaillée, 1h05min, problème avec mes fichiers et je n'arrivais pas à avancer dans le projet sinon j'aurais terminé en 5 minutes.

- style, 3 minutes, pas de difficulté et plus de facilité pour changer le style et savoir quel texte on change de style.

### question

Ajouter ce computed dans QuestionRadio.vue :

const answerText = computed<string>(
  () =>
    props.options.find((option) => option.value === props.answer)?.text ??
    props.answer,
);

Remplacer {{ props.answer }} par {{ answerText }} dans le template.

Expliquer pourquoi on a fait ce changement ainsi que le code du computed.

- En mettant une nouvelle variable, nous avons, tout d'abord, une meilleur lisibilité dans notre code et nous n'utilisons pas la variable directement, comme cela il n'y a pas de problème pour la variable props.answer, elle ne sera pas changer si on change la copie "answerText".

Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration.

- cela met un trait avec rien derrière car la chaine de caractère est vide dans nos questiontext et questionradio. ce n'est pas satisfaisant, on pourrait mettre une chaîne de caractère par défaut quand on met rien.

## semaine 6

### Temps passé

Tâche, Temps passé, Commentaire :

- Trivia, 3h environ, difficulté rencontré sur la bonne réponse. Même si l'utilisateur donnait la bonne réponse, c'était quand même écrit faux.

- QuestionCheckbox.vue, 45min

- ordre aléatoire dans QuestionRadio.vue, 1h30

- QuestionSelect.vue, 20min



### question et remarque

Expliquer votre démarche pour les améliorations que vous avez choisies :

Pourquoi avez-vous choisi ces améliorations ?

J'ai choisi de faire les améliorations suivantes : faire que le Trivia fonctionne comme mon quiz, QuestionCheckbox.vue, l'ordre aléatoire dans questionradio.vue et questionselect. 

j'ai fait le trivia car je trouvais intéressant de faire un autre quizform mais qui prenais des questions différentes à chaque fois et voir les différence que cela apporte au niveau du code pour implémenter les mêmes fonctionnalités, par exemple les boutons et le score.

j'ai fait le QuestionCheckbox car avoir plusieurs réponses dans un questionnaire est très utile dans un quiz est cela apportait un défi suplémentaire que de simplement avoir une seul réponse.

j'ai fait l'ordre aléatoire dans questionradio.vue car, tout d'abord, cela apportait de la difficulté lors du remplissage du quiz et, deuxièmement, j'ai remarqué que le trivia avait toujours la première réponse comme choix possible et donc ne donnait aucune difficulté dans le remplissage du trivia ce qui était dommage.

j'ai fait le QuestionSelect.vue car je trouvais plus esthétique que les questionradio.

je n'ai pas implémenté l'ordre des questions au hasard car j'avais peur que cela change plein de chose dans mon code et ainsi perdre toute ma progression.

Comment les avez-vous implémentées ?

Pour le trivia, je me suis inspiré de quizform, j'ai identifié les fonctions et les variables nécessaire pour pouvoir avoir les mêmes fonctionnnalités et la même forme général.

Pour Questioncheckbox.vue, j'ai remarqué une grande similitude avec QuestionRadio.vue donc j'ai repris les mêmes base et fait les changements nécessaire.

Pour l'ordre aléatoire dans les questions questionradio, j'ai fait les changements nécessaire dans questionradio.vue.

pour QuestionSelect.vue, j'ai fait la même raisonnement que QuestionCheckbox.vue.

Quels problèmes avez-vous rencontrés ?

j'avais, tout d'abord, commencé par faire trivia mais j'ai eu quelque problème quand je voulais faire les boutons, des fois il ne marchait pas et le dernier problème que j'ai eu est qu'il ne reconnaisait pas les bonnes réponses que l'utilisateur avait fait. J'avais toujours un score de 0/10 même lorsque je faisait un sans faute. j'avais finalement remarqué que l'implémentation de mon empty/wrong/correct était la première version que nous avions faite et ensuite c'était tout bon. 

Quelles améliorations pourriez-vous encore apporter ?

ordre aléatoire des questions et accepter plusieurs réponses possible pour QuestionText.vue. J'aurai aimé faire un dossier avec plusieurs quiz à l'intérieur (mais trop long et j'avais pas d'inspiration pour les questions).