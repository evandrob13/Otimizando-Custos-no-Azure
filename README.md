# Otimizando-Custos-no-Azure
"Portfólio de criação Otimizando Custos no Azure

from azure.identity import DefaultAzureCredential
from azure.mgmt.costmanagement import CostManagementClient
from datetime import datetime

# Configurando as credenciais e o cliente de gerenciamento de custos
credential = DefaultAzureCredential()
client = CostManagementClient(credential)

# Definir o escopo (substitua pelo ID da sua assinatura)
scope = "/subscriptions/<subscription_id>"

# Coletar dados de custos de um período específico
today = datetime.utcnow().isoformat()
cost_report = client.query.usage(
    scope,
    {
        "type": "ActualCost",
        "timeframe": "MonthToDate",
    }
)

# Exibir os custos
for item in cost_report.value.rows:
    print(f"Categoria: {item['UsageDate']}, Custo: {item['PreTaxCost']}")
