# Github 연동

## Procedure
### 1. Github
1. User Settings -> Developer settings
2. New OAuth App
3. Jenkins 등록하기
4. Client ID, Client Secret 저장하기


### 2. Jenkins
1. Jenkins 관리 -> Configure Global Security
2. 저장했던 Client ID, Client Secret 등록하기


### 3. Github
1. Repository Settings -> Webhooks
2. Add webhook
3. [JENKINS_URL]/github-webhook/