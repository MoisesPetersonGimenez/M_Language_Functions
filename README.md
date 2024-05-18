# M_Language_Functions
Objetivo desta função é agilizarmos a exclusão de colunas sem quaisquer registros.
(The purpose of this function is to speed up the deletion of columns without any records.)

(tabela as table) =>
let
    Fonte = tabela,
    Profile = Table.Profile (Fonte),
    VerificarColunasVazias = Table.AddColumn(Profile, "Dados", each [Count] - [NullCount], type number),
    ExcluirColunasVazias = Table.SelectRows(VerificarColunasVazias, each ([Dados] <> 0))[Column],
    ColunasSelecionadas = Table.SelectColumns (Fonte, ExcluirColunasVazias)
in
    ColunasSelecionadas
