---
tags:
  - ENG_REVERSA
---
# Assinatura de arquivo / bytes mágicos

As assinaturas de arquivos, comumente referidas como "portes mágicos", são sequências de bytes específicas no início de um arquivo que identificam ou verificam seu tipo de conteúdo e formato. Esses bytes geralmente têm caracteres ASCII correspondentes, permitindo uma legibilidade humana mais fácil quando inspecionados. O processo de identificação ajuda os aplicativos de software a determinar rapidamente se um arquivo está em um formato que eles podem manipular, auxiliando a funcionalidade operacional e as medidas de segurança.

Na segurança cibernética, as assinaturas de arquivos são cruciais para identificar tipos e formatos de arquivo. Você os encontrará em análise de malware, resposta a incidentes, inspeção de tráfego de rede, verificações de segurança da Web e análise forense. Saber como trabalhar com esses bytes mágicos pode ajudá-lo a identificar rapidamente atividades maliciosas ou suspeitas e escolher as ferramentas certas para uma análise mais profunda.

Aqui está uma lista de alguns dos arquivos mais comuns e sua magia:

|   |   |   |
|---|---|---|
|Formato do arquivo|Os Bytes da Magia|Representação ASCII|
|Arquivo de imagem PNG|89 50 4E 47 0D 0A 1A 0A|% PNG|
|Arquivo de imagem GIF|47 49 46 38|GIF8 (ta)|
|Executáveis Windows e DOS|4D 5A (Em and-s)|MZ em|
|Executáveis Linux ELF|7F 45 4C 46 Avaliações|.ELF (B)|
|Arquivo de áudio MP3|49 44 33||

