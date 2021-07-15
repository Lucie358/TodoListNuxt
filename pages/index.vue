<template>
  <v-app>
    <v-main>
      <v-container>
        <v-card class="mx-auto" max-width="400" elevation="2" tile>
          <v-list dense>
            <v-list-item-group>
              <!-- Pour chaque task dans mon tableau de tasks[] // On l'a appelé task, mais on aurait pu l'appeler tache-->
              <v-list-item v-for="(task, index) in tasks" :key="index">
                <v-list-item-content>
                  <v-list-item-title
                    >{{ task.name }} - {{ task.description }}
                    <v-list-item-icon>
                      <v-icon color="red" @click="removeTask(index)"
                        >mdi-delete</v-icon
                      >
                    </v-list-item-icon>
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
          <v-card-actions>
            <v-btn rounded color="primary" dark @click.stop="dialog = true">
              Ajouter une tâche
            </v-btn>
          </v-card-actions>
          <v-dialog v-model="dialog" max-width="290">
            <v-card>
              <v-card-title>Mon formulaire</v-card-title>
              <v-form>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field
                        v-model="taskName"
                        :counter="100"
                        label="Nom de la tâche"
                        required
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        v-model="taskDescription"
                        :counter="200"
                        label="Description de la tâche"
                        required
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-form>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="green darken-1" text @click="dialog = false">
                  Annuler
                </v-btn>
                <v-btn color="green darken-1" text @click="addTask">
                  Enregistrer
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "IndexTodoList",
  // On utilise un this que pour acceder a une autre fonction ou a data
  data() {
    return {
      dialog: false,
      taskName: "",
      taskDescription: "",
      tasks: []
    };
  },
  methods: {
    addTask() {
      // On veut prendre le contenu de taskName (qui se rempli grace au v-model dans la dialog)
      // Pour le mettre dans notre tableau de tasks qui est initialement vide, apres avoir cliqué sur enregistré
      // Notre taskname est =>    this.taskName
      // Un tableau d'objet :
      // tasks[
      //   0: {
      //     id: 0
      //     name: 'coucou',
      //     description: 'description'
      //   }
      //   1:
      // ]
      const completeTask = {
        name: this.taskName,
        description: this.taskDescription
      };
      this.tasks.push(completeTask);
      this.dialog = false;
      this.taskName = "";
    },
    removeTask(index) {
      // Retourne la position de task, dans notre tableau tasks.
      this.tasks.splice(index, 1);
    }
  }
};
</script>
