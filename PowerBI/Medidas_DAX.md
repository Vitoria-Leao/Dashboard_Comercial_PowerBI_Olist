# Fórmulas DAX utilizadas no dashboard

## Quantidade total de pedidos
Total de Pedidos = DISTINCTCOUNT(Fato_Vendas[order_id])

## Quantidade Total de Clientes
Clientes = COUNT(Dim_Clientes[customer_id])

## Ticket Médio total
Ticket Médio = DIVIDE([Receita Total],[Total de Pedidos],0)

## Receita Total
Receita Total = SUM(Fato_Vendas[price])

## Receita Média por Cliente
Receita Média por Cliente = DIVIDE([Receita Total],DISTINCTCOUNT(Fato_Vendas[customer_id]))

## Receita total para o estado de SP
Receita total para São Paulo = CALCULATE([Receita Total],Dim_Clientes[Estado] = "sao paulo")

## Receita total no ano anterior
Receita LY = CALCULATE([Receita Total],
                        SAMEPERIODLASTYEAR(Dim_Calendario[Date]))

## Porcentagem de crescimento em relação ao ano anterior
Crescimento % = DIVIDE([Receita Total]-[Receita LY],
                       [Receita LY])

## Quantidade Máxima de Pedidos por Cliente
Maximo de Pedidos = MAXX(VALUES(Fato_Vendas[customer_id]),
                         CALCULATE(DISTINCTCOUNT(Fato_Vendas[order_id]), 
                                   ALL(Fato_Vendas[order_id])))

## Quantidade Média de Pedidos por Cliente
Quantidade média de pedidos por cliente = DIVIDE(CALCULATE(DISTINCTCOUNT(Fato_Vendas[order_id]),
                                                           REMOVEFILTERS (Fato_Vendas)),
                                                 [Clientes],0)
