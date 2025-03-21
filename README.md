
# 📚 Guia de Build - JasperReports Library

Este guia explica como verificar e instalar o Java JDK e o Maven para compilar o projeto **JasperReports Library**.

---

## ✅ Passo 1: Verificar se o Java JDK está instalado
No terminal, execute:
```bash
java -version
```
Se aparecer algo como:
```
openjdk version "17.0.9"
```
O Java está instalado. Caso contrário, siga o passo 3.

---

## ✅ Passo 2: Verificar se o Maven está instalado
No terminal, execute:
```bash
mvn -version
```
Se o Maven estiver instalado, aparecerá a versão e o Java usado. Caso contrário, siga o passo 4.

---

## 🛠 Passo 3: Como instalar o Java JDK

### Linux (Debian/Ubuntu):
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

### Windows:
1. Baixe o JDK em [https://adoptium.net/](https://adoptium.net/)
2. Instale e selecione a opção **“Set JAVA_HOME”**
3. Verifique:
```bash
java -version
```

### macOS:
```bash
brew install openjdk@17
brew link --force --overwrite openjdk@17
```

---

## 🛠 Passo 4: Como instalar o Maven

### Linux (Debian/Ubuntu):
```bash
sudo apt install maven -y
```

### Windows:
1. Baixe em: [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)
2. Extraia para `C:\Program Files\Apache\Maven`
3. Adicione `MAVEN_HOME/bin` no `PATH`
4. Verifique:
```bash
mvn -version
```

### macOS:
```bash
brew install maven
```

---

## ✅ Passo 5: Compilando o Projeto
Dentro da pasta do projeto, execute:
```bash
mvn clean install source:jar javadoc:jar
```

Se houver alterações locais:
```bash
mvn clean install -Dmaven.buildNumber.doCheck=false
```

Para checar compatibilidade com JDK 1.8:
```bash
mvn clean install -Denforcer.skip=false -pl '!ext/ejbql, !ext/hibernate, !ext/servlets'
```

---

## ✅ Passo 6: Executar os Testes
```bash
mvn clean test
```

---

## ✅ Passo 7: Gerar a Documentação
Dentro da pasta `/docs`, execute:
```bash
cd docs
mvn clean compile
```
Documentação gerada em:
```
docs/target/docs
```

---

## 🎯 Fim!
Pronto! Agora você está preparado para compilar o JasperReports Library.
