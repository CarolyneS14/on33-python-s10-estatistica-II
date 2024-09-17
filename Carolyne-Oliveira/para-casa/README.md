# 📈📉📊🎲 Análises Estatística com Python - Testes de Hipóteses

## 📚 Descrição da Atividade

Exercicio para casa semana 10.

**Objetivo:** Por em prática os conhecimentos de Análise Estatística de Dados que aprendemos em aula.

Dado a planilha, quero saber com a confiança de 95% se as porcentagens de poluente na água caíram e se depois podemos afirmar com 95% de confiança que a poluição está em 85%

DESAFIO: Usando os dados do [Observatório dos Direitos Humanos](https://observadh.mdh.gov.br/), quero saber se tem mais heteros em um estado do que em outro.

## 📋 Passo a Passo

## 🟦 Atividade 1 - A porcentagem de poluente na água caiu?:

 ### - Bibliotecas Utilizadas:

        import pandas as pd
        import numpy as np
        from statsmodels.stats.weightstats import ztest
        import statsmodels.stats.weightstats as teste_hipotese
        from scipy.stats import ttest_rel
        from scipy.stats import ttest_1samp
        from scipy.stats import ttest_ind
        from scipy.stats import chi2_contingency
        from scipy.stats import chi2
        from scipy.stats import shapiro
        from scipy import stats
        import statistics

 ### - Coleta:

        # Baixando a base de dados
        poluicao = pd.read_excel('/content/Atividade ON33 - S10.xlsx')

        # Exibir as primeiras linhas do DataFrame
        print(poluicao.head())


 ### - Limpeza:

        # Converter uma coluna específica em uma lista
        poluicao_antes = poluicao['Antes'].tolist()

        # Exibir a lista
        print(poluicao_antes)

        # Converter uma coluna específica em uma lista
        poluicao_depois = poluicao['Depois'].tolist()

        # Exibir a lista
        print(poluicao_depois)  


 ### - Teste Estatístico:

        # Realizando o teste t pareado
        stats, p_value = ttest_rel(poluicao_depois, poluicao_antes, alternative="greater")

        #Exibir resultado dos testes
        print(f"T-stat: {stats}, p-value: {p_value}")

        confianca = 0.95

        significancia = 1 - confianca

        if p_value < significancia:
        print('Rejeitamos a Hipótese nula')
        else:
        print('Aceitamos a Hipótese nula')

## 🟦 Atividade 2 - Podemos afirmar com 95% de confiança que a poluição está em 85%?:        


 ### - Análises:

        # Calcular a média da poluição antes
        media_poluicao_antes = statistics.mean(poluicao_antes)

        # Exibir a média
        print(f"Média da poluição antes: {media_poluicao_antes}")

        # Calcular a média da poluição depois
        media_poluicao_depois = statistics.mean(poluicao_depois)

        # Exibir a média
        print(f"Média da poluição depois: {media_poluicao_depois}")

        # Calcular a média da poluição antes e depois
        media_poluicao_antes = np.mean(poluicao_antes)
        media_poluicao_depois = np.mean(poluicao_depois)

        # Calcular a média geral (antes e depois)
        media_poluicao_geral = (media_poluicao_antes + media_poluicao_depois) / 2

        # Exibir as médias
        print(f"Média da poluição antes: {media_poluicao_antes}")
        print(f"Média da poluição depois: {media_poluicao_depois}")
        print(f"Média geral: {media_poluicao_geral}")

 ### - Teste Estatístico:        

        # Executar o teste t pareado
        stats, p_value = ttest_rel(poluicao_antes, poluicao_depois, alternative="greater")

        # Exibir os resultados
        print(f'Estatística t: {stats:.4f}')
        print(f'Valor p: {p_value:.4f}')

        # Verificar se rejeitamos a hipótese nula
        confianca = 0.95

        significancia = 1 - confianca

        if p_value < significancia:
            print("Rejeitamos a hipótese nula. Há uma diferença significativa entre os níveis de poluição antes e depois.")
        else:
            print("Aceitamos a Hipótese nula. Não há uma diferença significativa entre os níveis de poluição antes e depois.")

## 🟦 DESAFIO - Existe mais heteros em um estado do que em outro?:

 ### - Coleta:

        LGBTQIAPN = pd.read_excel('/content/LGBTQIAPN+.xlsx')

        # Exibir as primeiras linhas do DataFrame
        print(LGBTQIAPN.head(7))

 ### - Análises:

        # Resumo do DataFrame
        LGBTQIAPN.info()

        #Criando um novo DF apartir da base LGBTQIAPN
        Heteros_Estado = ['Região', 'UF', 'Heterossexual', 'Bissexual']
        Heteros_Estado = LGBTQIAPN[Heteros_Estado]

        #Exibir novo DF só com as colunas selecionadas
        print(Heteros_Estado.head(28))

        # Contar o número total de valores nulos no DataFrame
        total_nulos = Heteros_Estado.isnull().sum().sum()
        print(f'Total de valores nulos: {total_nulos}')

 ### - Teste Estatístico:  

        # Teste de hipóteses
        chi2_stat, p_value, dof, expected = chi2_contingency(Heteros_Estado['Heterossexual'], Heteros_Estado['Bissexual'])

        # Exibir os resultados
        print(f"Estatística do qui-quadrado: {chi2_stat:.4f}")
        print(f"Valor p: {p_value:.4f}")

        # Verificar se rejeitamos a hipótese nula
        confianca = 0.95

        significancia = 1 - confianca

        if p_value < significancia:
            print("Rejeitamos a hipótese nula. Há uma diferença significativa entre Heterossexuais e Bissexuais por estado.")
        else:
            print("Aceitamos a Hipótese nula. Não há uma diferença significativa entre Heterossexuais e Bissexuais por estado.")

  
## 👩🏻‍🏫 Professora Daniele Fernandes Rodrigues Junior.
<br/>
[Linkedin](https://www.linkedin.com/in/daniele-fernandes-rodrigues-junior-8244bb24/)
