# Nosql
#Disciplina Pós Data Science NoSql

#Atividade Prática – HBase

#Exercício 1

#Agora, de dentro da imagem faça os sefuintes procedimentos:

1.	 create 'italians', 'personal-data', 'professional-data'

2.	hbase shell /tmp/italians.txt’

#Agora execute as seguintes operações:


1.	hbase(main):006:0> put 'italians', '11', 'personal-data:city', 'Blumenau'
Took 0.0051 seconds
hbase(main):007:0> put 'italians', '12', 'personal-data:city', 'Blumenau'
Took 0.0033 seconds
hbase(main):008:0> put 'italians', '11', 'personal-data:data_nascimento', '02-04-1988'
Took 0.0030 seconds
hbase(main):009:0>  put 'italians', '12', 'personal-data:data_nascimento', '14-10-1984'
Took 0.0030 seconds
hbase(main):010:0>  put 'italians', '11', 'personal-data:role', 'Tecnologia de Informacao'
Took 0.0031 seconds
hbase(main):011:0> put 'italians', '12', 'personal-data:role', 'Saude'
Took 0.0031 seconds
hbase(main):012:0> put 'italians', '11', 'personal-data:anos_de_experiencia', '14'
Took 0.0032 seconds
hbase(main):013:0> put 'italians', '12', 'personal-data:anos_de_experiencia', '12'
Took 0.0039 seconds

2.	hbase(main):014:0> alter 'italians', NAME => 'personal-data', VERSIONS => 5
Updating all regions with the new schema...
1/1 regions updated.
Done.
Took 2.2035 seconds


3.	put 'italians', '12', 'personal-data:name', 'Aline Bompani'

put 'italians', '12', 'personal-data:city', 'Massaranduba'

put 'italians, '11', 'personal-data:city', 'Lages'

' put 'italians, '12', 'personal-data:anos_de_experiencia', '17'

put 'italians', '12', 'personal-data:city', 'Sao Paulo'

4.	hbase(main):001:0> get 'italians', '12', {COLUMN => 'personal-data:city', VERSIONS => 4}
COLUMN                          CELL
 personal-data:city             timestamp=1588346406723, value=Massaranduba
 personal-data:city             timestamp=1588345538427, value=Blumenau
1 row(s)

5. hbase(main):019:0> scan 'italians', { COLUMNS => ['personal-data:name', 'professional-data:role'] }
ROW                                    COLUMN+CELL
 10                                    column=personal-data:name, timestamp=1588344670153, value=Giovanna Caputo
 10                                    column=professional-data:role, timestamp=1588344670166, value=Comunicacao Institucional
 12                                    column=personal-data:name, timestamp=1588346344847, value=Aline Bompani
 2                                     column=personal-data:name, timestamp=1588344669916, value=Domenico Barbieri
 2                                     column=professional-data:role, timestamp=1588344669932, value=Psicopedagogia
 4                                     column=personal-data:name, timestamp=1588344669975, value=Silvia Gallo
 4                                     column=professional-data:role, timestamp=1588344669989, value=Engenharia Industrial Madeireira
 6                                     column=personal-data:name, timestamp=1588344670044, value=Simone Lombardo
 6                                     column=professional-data:role, timestamp=1588344670060, value=Biotecnologia e Bioquimica
 8                                     column=personal-data:name, timestamp=1588344670098, value=Simone Ferrara
 8                                     column=professional-data:role, timestamp=1588344670112, value=Engenharia de Minas
6 row(s)
Took 0.0818 seconds

6. hbase(main):011:0> deleteall 'italians', '1'
Took 0.0424 seconds
hbase(main):012:0> deleteall 'italians', '3'
Took 0.0032 seconds
hbase(main):013:0> deleteall 'italians', '5'
Took 0.0045 seconds
hbase(main):014:0> deleteall 'italians', '7'
Took 0.0037 seconds
hbase(main):015:0> deleteall 'italians', '9'
Took 0.0046 seconds
hbase(main):016:0> deleteall 'italians', '11'
Took 0.0033 seconds
hbase(main):017:0>

7. hbase(main):020:0> put 'italians', '5', 'personal-data:name', 'Terezinha Rotta'
Took 0.0150 seconds
hbase(main):028:0> put 'italians', '5', 'personal-data:idade', 65
Took 0.0040 seconds
