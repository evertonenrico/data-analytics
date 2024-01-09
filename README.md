# Data Analytics

Projeto realizado para o controle de notas e médias dos alunos de uma escola.

Para o retorno das <b>notas</b> foi utilizado o código DAX abaixo:

```c++
Media de Notas = 
--Media da Frente
VAR MF = 
        TRUNC(
        AVERAGEX(VALUES(FACT_Notas[FrenteNome]),[Media Ponderada]),
        2)
        

 --Valida se tem Média de REC
VAR RECDISC =
    TRUNC(
        (CALCULATE(
        DIVIDE(
            SUMX(FACT_Notas,(FACT_Notas[Peso]*FACT_Notas[Nota])),
            SUMX(FACT_Notas,FACT_Notas[Peso])
        ),
        FACT_Notas[TipoAvaliacao] = "RECDISC" || FACT_Notas[TipoAvaliacao] = "RECFRT"

    )),2)

--Cálculo da Media x Rec
VAR MFINAL = 
    IF (
     RECDISC <> BLANK(),
    (RECDISC + MF) / 2, MF
    )

--Média Final, verifica se é maior que REC
VAR MEDIA = 

    IF (
        MFINAL > MF , TRUNC (MFINAL,1),MF
    )

VAR Unif = 
    (CALCULATE(
        DIVIDE(
            SUMX(FACT_Notas,(FACT_Notas[Peso]*FACT_Notas[Nota])),
            SUMX(FACT_Notas,FACT_Notas[Peso])
        ),
        FACT_Notas[TipoAvaliacao] = "UNIF" 
        )
    )

var MediaFinal = 
    IF(
        Unif <> BLANK(),MEDIA + Unif, 
            MEDIA
    )

return 

    if(
        MediaFinal > 10,10,MediaFinal
    )

```

<img src="https://i.ibb.co/DQZRNT4/TELA-001.png" alt="Tela de Notas e Médias" border="0">
