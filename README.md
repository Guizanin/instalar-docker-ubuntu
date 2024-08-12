# instalar-docker-ubuntu | tutorial retirado [educoutinho](https://educoutinho.com.br/windows/instalando-docker-no-wsl/)


* Presumo que tenho instalado o WSL ou esteja no Ubuntu

## Pré instalação

### ☑️ verificando versão Ubuntu
~~~
cat /etc/os-release
~~~

### ☑️ Utilizar iptables legadas
~~~
sudo update-alternatives --config iptables
~~~
* Selecionar a opção “iptables-legacy”


## Instalar o Docker

### ☑️ Remover versões antigas
~~~
sudo apt-get remove docker docker-engine docker.io containerd runc
~~~

### ☑️ Se não tiver docker instalado, vai exibir: “Unable to locate package docker-engine”
### Intando dependências 
#### copiar todas as linhas e colar no terminal
~~~
sudo apt-get update -y && sudo apt-get upgrade -y &&
sudo apt-get install ca-certificates curl gnupg lsb-release -y && 
sudo apt-get autoremove -y
~~~
* o '-y' para confirmar que sim caso algum comando necessite e o '&&' é a forma de concatenar os comando em um só'

### ☑️ Adicionar chave do repositório oficial do Docker
~~~
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
~~~

### ☑️  Instalar o Docker Engine
~~~
sudo apt-get update -y &&
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
~~~

### ☑️ Testando a instalação
~~~
docker --version && docker compose version
~~~


## Adicionar Alias

* Alias para o comando “docker-compose” funcionar ao invés de toda vez ter que digitar '_docker compose_...'

### ☑️ Abrir o arquivo
~~~
nano ~/.bash_aliases
~~~

### ☑️ Adicionar a seguinte linha
~~~
alias docker-compose="docker compose"
~~~
* Salvar o arquivo pressionando CTRL+X

### ☑️ Execute
~~~
source ~/.bash_aliases
~~~

### ☑️ Teste agora
~~~
docker-compose version
~~~


## Adicionar permissões

### ☑️ Execute
~~~
sudo groupadd docker && sudo usermod -aG docker $USER
~~~


## Executando

### ☑️ Stopando qualquer serviço docker que poça estar ativo
~~~
sudo service docker stop
~~~

### ☑️ Iniciar o Docker
~~~
sudo dockerd
~~~
