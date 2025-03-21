
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

## ✅ Passo 5: Informações sobre o Projeto JasperReports Library

O projeto JasperReports Library consiste em um artefato core JAR e vários artefatos opcionais de extensão JAR.

O sistema de build depende exclusivamente do **Maven**.

Para compilar o core e as extensões, execute na raiz do projeto:
```bash
mvn clean install source:jar javadoc:jar
```

Se o projeto tiver modificações locais não commitadas no Git:
```bash
mvn clean install -Dmaven.buildNumber.doCheck=false
```

Para garantir a compatibilidade com o JDK 1.8:
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

## ✅ Passo 8: Executar os Exemplos (Samples)

O projeto possui diversos exemplos (samples) para demonstrar funcionalidades.

### Iniciar o banco de dados HSQLDB (requerido por alguns samples):
```bash
cd demo/hsqldb
mvn exec:java
```

### Executar um sample individual:
```bash
cd demo/samples/<nome_do_sample>
mvn clean compile exec:java
```

### Executar um método específico do sample (exemplo gerar PDF):
```bash
mvn exec:java -Dexec.args=pdf
```

### Executar vários métodos na sequência:
```bash
mvn exec:java -Dexec.args="pdf xls"
```

### Visualizar o design do relatório JRXML:
```bash
mvn exec:java@viewDesign
```

### Visualizar o arquivo compilado .jasper:
```bash
mvn exec:java@viewDesign -Dexec.args=target/reports/I18nReport.jasper
```

### Visualizar o arquivo .jrprint gerado:
```bash
mvn exec:java@view
# Ou especificando o arquivo:
mvn exec:java@view -Dexec.args=target/reports/I18nReport.jrprint
```

### Também funciona para arquivos XML exportados:
```bash
mvn exec:java@view -Dexec.args=target/reports/I18nReport.jrpxml
```

### Executar um sample completo incluindo todos os serviços necessários:
```bash
mvn clean compile exec:exec@all
```

### Executar todos os samples de uma vez (na pasta /demo/samples):
```bash
cd demo/samples
mvn clean compile exec:exec@all
```

---

## 🎯 Fim!
Pronto! Agora você tem o ambiente configurado para compilar, testar, gerar documentação e executar os exemplos do JasperReports Library.
