KAPICÚA - APP LINKS / UNIVERSAL LINKS

SUBIR AL REPO QUE PUBLICA:
https://mikhailpolozhaev.github.io/

ESTRUCTURA:
/
├── .nojekyll
├── .well-known/
│   ├── assetlinks.json
│   └── apple-app-site-association
└── kapicua/
    └── sala/
        └── index.html

IMPORTANTE:
Usa este formato de enlace:
https://mikhailpolozhaev.github.io/kapicua/sala/?id=ABC123

No uses /sala/ABC123 porque GitHub Pages es estático y puede dar 404.

ANDROID
1. En .well-known/assetlinks.json reemplaza:
REEMPLAZAR_CON_SHA256_DE_GOOGLE_PLAY

por la SHA-256 del Certificado de firma de aplicación de Google Play.
Package preparado:
com.polozhaev.dominicandom

2. En Android necesitas un intent-filter con:
android:autoVerify="true"
scheme=https
host=mikhailpolozhaev.github.io
pathPrefix=/kapicua/sala/

IOS
1. En .well-known/apple-app-site-association reemplaza:
REEMPLAZAR_TEAM_ID
REEMPLAZAR_BUNDLE_ID_IOS

2. En Xcode:
Signing & Capabilities → Associated Domains
Añade:
applinks:mikhailpolozhaev.github.io

UNITY
Comparte así:

public void OnClickCompartirSala()
{
    if (string.IsNullOrEmpty(salaId)) return;

    string link = $"https://mikhailpolozhaev.github.io/kapicua/sala/?id={UnityWebRequest.EscapeURL(salaId)}";
    string mensaje = $"¡Únete a mi partida de Kapicúa!\nCódigo de sala: {salaId}\n{link}";

    Application.OpenURL(
        "https://wa.me/?text=" + UnityWebRequest.EscapeURL(mensaje)
    );
}

DeepLinkManager debe aceptar:
kapicua://sala/ABC123
y
https://mikhailpolozhaev.github.io/kapicua/sala/?id=ABC123

PRUEBAS
Comprueba que abren sin redirección:
https://mikhailpolozhaev.github.io/.well-known/assetlinks.json
https://mikhailpolozhaev.github.io/.well-known/apple-app-site-association

Y:
https://mikhailpolozhaev.github.io/kapicua/sala/?id=TEST123

NOTA IOS
Apple espera el archivo AASA por HTTPS y sin redirecciones. Comprueba también el Content-Type del archivo apple-app-site-association. Si GitHub Pages no lo sirve con un tipo aceptable, habrá que alojar ese archivo en un hosting donde se pueda fijar application/json.
