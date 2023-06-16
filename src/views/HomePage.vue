<template>
  <ion-page>
    <ion-content :fullscreen="true">

      <div id="container">
        <ion-button @click="note">Trigger Haptic Feedback</ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { LocalNotifications } from '@capacitor/local-notifications';
export default {
    components: { LocalNotifications },
    data() {
      return {
        localNotifications: LocalNotifications,
      };
    },
    methods: {
      async note() {
        await LocalNotifications.registerActionTypes({
          types: [
            {
              id: 'your_choice',
              actions: [
                {
                  id: 'dismiss',
                  title: 'Dismiss',
                  destructive: true
                },
                {
                  id: 'open',
                  title: 'Open app'
                },
                {
                  id: 'respond',
                  title: 'Respond',
                  input: true
                }
              ]
            }
          ]
        });

        console.log(this.localNotifications);
        this.localNotifications.schedule({
          id: 1,
          text: 'Single LocalNotification',

          data: { secret: key },
        });
      },
    },
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
