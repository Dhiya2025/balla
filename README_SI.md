# Mini Walkie Talkie — Render free deploy project

මෙය Android Push-to-Talk සහ room text messages සඳහා සරල client/server prototype එකකි. Android project එක `app/` තුළත්, Node.js WebSocket relay එක `server/` තුළත් ඇත. එක room එකකට උපරිම 10 දෙනෙකුට සම්බන්ධ විය හැක.

## Render free deploy කිරීම

1. මේ project එක ඔබේ GitHub repository එකකට upload/push කරන්න. Repository root එකේ `render.yaml` තිබිය යුතුය.
2. Render dashboard එකේ **New → Blueprint** තෝරා repository එක connect කරන්න.
3. Render විසින් Blueprint එකෙන් `mini-walkie-talkie-relay` Free web service එක සාදා `server/` folder එක build කර deploy කරයි.
4. Deploy සාර්ථක වූ පසු service එකේ URL එක මෙවැනි වේ: `https://mini-walkie-talkie-relay.onrender.com` (Render විසින් නම වෙනස් කළ හැක).
5. Android app එක විවෘත කර **Render server address** තැනට Render Dashboard එකේ පෙන්වන URL එක paste කර **CONNECT TO ROOM** ඔබන්න. `https://` එක app එක ස්වයංක්‍රීයව secure WebSocket `wss://` බවට පරිවර්තනය කරයි. URL එක device එකේ save වන නිසා නැවත ඇතුළත් කිරීමට අවශ්‍ය නැත.
6. ඔබේ නම සහ room එක තෝරන්න. එම room එකට එන අයට එකම room නම භාවිතා කළ යුතුය. Android microphone permission එක ලබා දෙන්න.

Health check එක `https://YOUR-SERVICE.onrender.com/health` මඟින් පරීක්ෂා කළ හැක. [Render free-plan සීමා](https://render.com/docs/free) සහ [Render WebSocket මඟපෙන්වීම](https://render.com/docs/websocket) බලන්න.

## Free සේවාවේ සීමා

Render free web service එක විනාඩි 15ක් inbound traffic නොලැබුණොත් spin down වේ. ඊළඟ connection එකේ service එක නැවත ආරම්භ වන තෙක් සාමාන්‍යයෙන් විනාඩියක් පමණ බලා සිටීමට සිදු විය හැක. App එක retry කරමින් status පෙන්වයි. Free service එක hobby/testing සඳහා සුදුසු නමුත් production හෝ හදිසි සන්නිවේදනය සඳහා uptime සහතිකයක් නොවේ.

## APK build කිරීම

Android Studio වල project folder එක open කර sync කරන්න. Debug APK එක `app/build/outputs/apk/debug/app-debug.apk` තුළ ලැබේ. Command line එකෙන් `./gradlew assembleDebug` ධාවනය කළ හැක. Android SDK සහ JDK අවශ්‍ය වේ.

## වැදගත් ආරක්ෂක සටහන

මෙය මුල් prototype එකකි. Server එකේ login/authentication, room password, user identity verification, moderation සහ privacy control නැත. Server URL එක දන්නා ඕනෑම අයෙකුට room නම දැනගත් විට එයට join විය හැක. Render `wss://` මඟින් ගමනාගමනය TLS හරහා ආරක්ෂා කළත්, app-level voice encryption හෝ end-to-end encryption මෙහි නැත. පුද්ගලික හෝ සංවේදී සංවාද සඳහා මෙය භාවිතා නොකරන්න. Free instance එක restart විය හැකි නිසා සම්බන්ධතාවය අතරමඟ වැටෙන්නත් පුළුවන.

Voice audio එක 16 kHz mono PCM ලෙස relay කරයි; එබැවින් data usage එක WebRTC/Opus solution එකකට වඩා වැඩි විය හැක.
