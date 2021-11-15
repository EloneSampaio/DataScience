# Documentação

As funções de agregação SUM () e AVG () não funcionam com valores temporais. (Eles convertem os valores em números, o que perde a parte após o primeiro caractere não numérico.) Para contornar esse problema, você pode converter em unidades numéricas, executar a operação de agregação e converter novamente em um valor temporal.

Exemplos:
SELECT SEC_TO_TIME (SUM (TIME_TO_SEC (time_col))) FROM nome_tabela;

SELECT FROM_DAYS (SUM (TO_DAYS (date_col))) FROM tbl_name;


# Sites acessados

https://www.dataindependent.com/pandas/pandas-to-datetime/
https://realpython.com/pandas-groupby/
https://www.geeksforgeeks.org/python-pandas-dataframe-isin/
https://www.geeksforgeeks.org/ways-to-filter-pandas-dataframe-by-column-values/
https://www.codeforests.com/2020/07/18/calculate-percentage-within-group/
https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.agg.html?highlight=agg

https://towardsdatascience.com/6-pandas-display-options-you-should-memories-84adf8887bc3#:~:text=Set%20Max%20Number%20of%20Rows&text=The%20default%20number%20is%2060,the%20middle%20will%20be%20truncated.&text=If%20we%20set%20the%20option,the%20rows%20will%20be%20displayed.


https://www.py4u.net/discuss/154795
