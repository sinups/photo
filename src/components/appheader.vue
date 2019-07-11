<template>
  <span>
     <v-navigation-drawer app v-model="drawer" class="dark lighten-3" dark disable-resize-watcher>
            <v-list>
                <template v-for="(item, index) in items">
                    <v-list-tile :key="index">
                        <v-list-tile-content>
                            {{item.title}}
                        </v-list-tile-content>
                    </v-list-tile>
                    <v-divider :key="`divider-${index}`"></v-divider>
                </template>
            </v-list>
        </v-navigation-drawer>
    <v-toolbar app flat dark color="teal lighten-3">
       <v-toolbar-side-icon class="hidden-md-and-up" @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="headline text-uppercase">
        <span>photo</span>
        <span class="font-weight-light">bank</span>
      </v-toolbar-title>
       <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat>Пользователь</v-btn>
        <v-btn flat>Сохранение</v-btn>
        <v-btn flat>О приложении</v-btn>
        <v-btn flat>Контакты</v-btn>
      </v-toolbar-items>
    </v-toolbar>
  </span>
</template>
<script>
export default {
   name: 'appheader',
    data() {
        return {
            drawer: false,
            items: [
                { title: 'Пользователь' },
                { title: 'Сохранение' },
                { title: 'О приложении' },
                { title: 'Контакты' }
            ]
        };
    },
};
</script>

<style>
</style>
