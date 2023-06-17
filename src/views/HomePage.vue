<template>
  <ion-page>
    <ion-content :fullscreen="true">

      <div id="container">
        <ion-input type="text" v-model="title" placeholder="Title"></ion-input>
        <ion-input type="text" v-model="body" placeholder="Msj"></ion-input>
        <ion-button @click="scheduleNotification">Trigger Haptic Feedback</ion-button>        
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { LocalNotifications } from '@capacitor/local-notifications';

export default {
  data () {
      return {
          logo:import.meta.env.BASE_URL+"favicon.png",
          sound:import.meta.env.BASE_URL+"sound.mp3",
          title:"Title",
          body:"Body",
      }
  },
  methods: {
    async scheduleNotification() {
        const result = await LocalNotifications.requestPermissions();
        if (result.display == "granted") {
          const notif = await LocalNotifications.schedule({
            notifications: [
              {
                title: this.title,
                body: this.body,
                id: 1,
                schedule: { at: new Date(Date.now() + 1000) },
                playSound: true, // activa la reproducción de sonido configurado por el teléfono
                // sound: this.sound, // ruta del archivo de sonido
                // smallIcon: "res://ic_stat_icon_name", // ruta de la imagen del icono pequeño                
                smallIcon: this.logo,
                vibrate: true // activa la vibración en la notificación
              }
            ]        
          });
          console.log('Notificación programada con éxito', notif);
        } else {
          console.log('Permiso para mostrar notificaciones denegado');
        }
    }
  }
}
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
