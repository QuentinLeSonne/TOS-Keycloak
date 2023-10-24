# TOS-Keycloak sur Kubernetes avec Helm

Sur votre Master, installez Keycloak avec helm :
Le fichier values.yaml est disponible dans le repo.

```
helm repo add bitnami https`h://charts.bitnami.com/bitnami
helm repo update
helm install keycloak bitnami/keycloak -f values.yaml --namespace keycloak-system 
kubectl get pods --namespace keycloak-system
kubectl get services --namespace keycloak-system
```

Il faut ensuite se rendre sur le keycloak, avec l'url : ip_du_serveur:port
- Créez un realm `digital-jukebox-front`
- Créez un client `digital-jukebox-client`
   - Dans la partie name `${client_account}`
   - Dans la partie root url et home url : `http://votre_ip:votre_port/admin/digital-jukebox-keycloak/console/`
   - Activez "client authentification", "autorization", "strandard flow", "direct access grant"
- Créez un user
   - Définir un user, un mail, un nom et un prénom
   - Dans credentials, définir un password
- Dans Realm settings, définir un id "digital-jukebox-keycloak"
   - Définir un display name "digital-jukebox-front"
   - Dans login, cochez "User registration", "forgot password", "remember me", "login with email"
- Créez un flow dans authentification "digital-jukebox-auth"
   - Allow access [Required]
   - Reset password [Disabled]
   - Username Password form for identity provider reauthentification [Required]
- Dans identity provider, créez le provider github et insérez le le client id et le client secret
   - Dans votre compte github, vous pouvez générer ces informations dans Settings > Developper settings > New github app > Définir un nom, mettre l'url d'authentification keycloak et l'url de retour si connexion réussi
