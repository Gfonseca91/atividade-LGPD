import pandas as pd

# Carregando os dados originais
df_beneficio = pd.read_csv("/content/beneficios_saude.csv")
df_cliente = pd.read_csv("/content/clientes.csv")
df_compra = pd.read_csv("/content/compras.csv")

# Gerando o conteúdo de um README campeão para o projeto
readme_content = """# 📊 Pipeline de Integração de Dados & Conformidade LGPD

Este projeto demonstra a criação de uma pipeline robusta de ETL (Extract, Transform, Load) utilizando Python e Pandas. O objetivo é integrar diferentes bases de dados corporativas (Benefícios, Clientes e Compras) e aplicar técnicas de anonimização e tratamento de dados para garantir a conformidade com a **LGPD (Lei Geral de Proteção de Dados)**.

## 🛠️ Tecnologias Utilizadas
- **Python 3**
- **Pandas**: Manipulação, limpeza e transformação de dados estruturados.

## 📂 Estrutura dos Dados
O projeto consome três conjuntos de dados principais localizados em `/content/`:
1. **`clientes.csv`**: Informações cadastrais de clientes (`cliente_id`, `nome`, `cpf`, `email`, `idade`, `cep`).
2. **`beneficios_saude.csv`**: Dados de planos de saúde corporativos (`cpf`, `plano_saude`, `condicao_cronica`).
3. **`compras.csv`**: Registro de transações financeiras (`transacao_id`, `cliente_id`, `valor_gasto`, `categoria`).

## 🔄 Etapas do Processo

### 1. Carga de Dados
Os dados são importados diretamente de arquivos CSV de forma eficiente utilizando as facilidades de I/O do Pandas.

### 2. Cruzamento de Dados (Merge Multitabelas)
Como os dados vêm de diferentes sistemas, a consolidação ocorre em duas etapas consecutivas para garantir integridade referencial:
- **Etapa 1**: Associação de Clientes e Benefícios utilizando a chave natural `cpf`.
- **Etapa 2**: Associação do resultado anterior à tabela de Compras utilizando a chave substituta `cliente_id`.

### 3. Governança & Conformidade LGPD
Para garantir a privacidade dos clientes e evitar a exposição desnecessária de dados pessoais identificáveis (PII):
- **Filtro de Atributos**: Descarte de colunas sensíveis como `nome`, `cpf` e `email` para análises de negócios.
- **Mascaramento de CEP**: Mascaramento dos dígitos finais do CEP para impedir a reidentificação geográfica precisa, mantendo a utilidade para análises regionais amplas.
- **Agrupamento Etário (Binning)**: Criação de faixas etárias personalizadas (`18-25`, `26-35`, `36-50`, `60+`) a partir da idade exata para proteger a identidade individual.

---
Desenvolvido com foco em boas práticas de engenharia de dados e governança corporativa.
"""

with open("README.md", "w", encoding="utf-8") as f:
    f.write(readme_content)

print("README.md criado com sucesso!")
