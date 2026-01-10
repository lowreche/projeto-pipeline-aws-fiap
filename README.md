# AWS na Prática: Pipeline CI/CD Serverless 🚀
### Pós-Tech FIAP | DevOps & Arquitetura Cloud

Este repositório contém o laboratório prático para a disciplina **AWS na Prática**. O objetivo é demonstrar a implementação de uma esteira de entrega contínua (CD) utilizando serviços de nuvem e automação de infraestrutura.

## 📋 Visão Geral
O projeto consiste na hospedagem de um site estático no **Amazon S3**, com deploy automatizado via **GitHub Actions**. Esta arquitetura exemplifica os pilares de agilidade, confiabilidade e redução de Time-to-Market discutidos em aula.

## 🏗️ Arquitetura da Solução
A solução segue o modelo de arquitetura integrada:
1.  **Controle de Versão:** GitHub (Source de Verdade).
2.  **CI/CD Orchestrator:** GitHub Actions (Gatilho automático a cada `push`).
3.  **Hospedagem (Hosting):** Amazon S3 (Static Website Hosting).
4.  **Segurança:** AWS IAM com credenciais temporárias via GitHub Secrets.

## 🛠️ Tecnologias Utilizadas
* **AWS S3:** Armazenamento de objetos e hosting serverless.
* **GitHub Actions:** Automação de workflow e integração contínua.
* **AWS CLI:** Interface de linha de comando para sincronização de artefatos.
* **HTML5/CSS3:** Frontend da aplicação demonstrativa.

## 🚀 Como Executar este Laboratório

### 1. Preparação na AWS (S3)
* Crie um bucket S3 com o nome `lab-pipeline-luizreche-2026`.
* Habilite a **Hospedagem de site estático**.
* Desative o "Bloqueio de acesso público" e aplique a **Bucket Policy** para leitura pública (vc pode encontrar o arquivo s3policy.json na main deste repositório):
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::lab-pipeline-luizreche-2026/*"
            }
        ]
    }
    ```

### 2. Configuração de Secrets no GitHub
Para que a pipeline tenha permissão de escrita no S3, adicione as seguintes chaves em `Settings > Secrets and variables > Actions`:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_SESSION_TOKEN` (Obrigatório em ambientes Vocareum/AWS Academy)

### 3. Deploy Automatizado
Qualquer alteração realizada no arquivo `index.html` e enviada para a branch `main` disparará o workflow automaticamente:
```bash
git add .
git commit -m "feat: upgrade design profissional"
git push origin main
