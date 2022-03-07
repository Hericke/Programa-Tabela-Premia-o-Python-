# Programa-Tabela-Premia-o-Python-
Aviso por SMS de cota batida do vendedor 
A ideia do progarma e vericar as tabelas de vendas dos meses e adicionar uam premiação 
que e envida por SMS quana a meta for batida no mes subsequente esse e meu segundo projeto em python e realmente estou feliz 
com o resultado porem eu sei que tenho que melhorar muito ...

import pandas as pd
from twilio.rest import Client

# Your Account SID from twilio.com/console
account_sid = "ACf1517cd2f82569f82f16aa7d2a4d578c"
# Your Auth Token from twilio.com/console
auth_token  = "801ffc0436e656b6c19e0d3c093518bf"
client = Client(account_sid, auth_token)


# Abrir os arquivos em Excel

lista_meses = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho']

for mes in lista_meses:
    tabela_vendas = pd.read_excel(f'{mes}.xlsx')
    if (tabela_vendas['Vendas'] > 36000).any():
        vendedor = tabela_vendas.loc[tabela_vendas['Vendas'] > 36000, 'Vendedor'].values[0]
        vendas = tabela_vendas.loc[tabela_vendas['Vendas'] > 36000,  'Vendas'].values[0]
        print(f'No mes {mes} alguem bateu a meta. Vendedor: {vendedor}, Vendas: {vendas}')
        message = client.messages.create(
            to="+11947012805",
            from_="+16626676321",
            body=f'No mes {mes} alguem  bateu a meta. Vendedor: {vendedor}, Vendas: {vendas}')

        print(message.sid)

# Para cada arquivo na coluna de vendas e mair de 36,000 mil

# se for maior que 36 mil enviar sms com o nome e o mes da vendas do vendedor

# se nao for mair do que 36 mil nao fazer nada



