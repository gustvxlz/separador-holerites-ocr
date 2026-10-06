# Separador de Holerites com OCR

Ferramenta em HTML e JavaScript para separar lotes de holerites em PDF, identificar funcionários, associar os nomes a uma planilha CSV e baixar os arquivos renomeados em ZIP.

## Como usar

1. No GitHub, clique em **Code → Download ZIP** e extraia a pasta.
2. Abra `index.html` no navegador, com acesso à internet para carregar as bibliotecas e o modelo de OCR.
3. Envie um CSV com as colunas `nome` e `cpf`. O CPF deve ser texto para preservar zeros no início.
4. Selecione ou arraste os PDFs.
5. Clique em **Processar holerites** e confira a tabela de resultados e as mensagens do processamento.
6. Clique em **Baixar .zip**.

Se o navegador impedir o carregamento a partir de um arquivo local, você pode servir a pasta com Python:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Abra `http://localhost:8000` no mesmo computador.

## Recursos

- Extração da camada de texto dos PDFs.
- OCR em português quando o nome não é identificado pelo texto.
- Associação por nome exato, palavras do nome e similaridade aproximada.
- Separação das páginas e geração de PDFs individuais.
- Nomes de arquivos no formato `CPF_NOME.pdf`.
- Pastas `holerites_renomeados` e `sem_cpf` dentro do ZIP.
- Preferência por PDFs avulsos de uma página ao resolver duplicatas; em empates de tamanho do PDF, o último arquivo enviado tem prioridade.
- Camada de texto invisível nos PDFs que passaram por OCR.
- Armazenamento do CSV neste navegador e botão **Remover** para apagá-lo.

## Processamento e dados

O código processa os PDFs e o CSV no navegador, sem implementar envio desses documentos para um servidor. As bibliotecas, fontes e o modelo de OCR são carregados de serviços externos; portanto, o programa depende de internet e não é uma distribuição completamente offline.

O CSV com nomes e CPFs permanece no armazenamento local do navegador até ser removido pela interface ou pela limpeza dos dados do navegador. Ao usar um computador compartilhado, remova-o depois do trabalho.

Este repositório contém somente o programa e a documentação. Não inclui holerites, cadastro de funcionários ou dados reais. O `.gitignore` exclui PDFs, CSVs, planilhas e ZIPs de trabalho.

## Limitações

- OCR e associação aproximada podem reconhecer nomes incorretamente. Confira os resultados antes de distribuir os holerites.
- Páginas sem nome identificado são puladas e informadas no log.
- O programa seleciona uma página por nome normalizado; documentos de várias páginas por funcionário precisam de adaptação.
- CPFs são normalizados para dígitos, sem validação dos dígitos verificadores.
- O parser é voltado a layouts de holerite com nome do funcionário e informações numéricas na mesma linha, com busca alternativa pelos nomes do CSV.
- PDFs gerados acima de aproximadamente 2,5 MB são rasterizados para reduzir o tamanho, o que pode alterar a qualidade e a camada de texto original.

## Bibliotecas

Papa Parse, PDF.js, pdf-lib, JSZip e Tesseract.js, carregadas pelas URLs definidas em `index.html`. A interface também utiliza fontes do Google Fonts.

## Licença

Distribuído sob a [licença MIT](LICENSE). Você pode usar, modificar e distribuir o programa, inclusive comercialmente, mantendo o aviso de autoria e a licença. As bibliotecas de terceiros continuam sujeitas às respectivas licenças.
