# Hello-world
My first repository in GitHub
creating new branch
USE BBIAPPS

GO

SELECT  *

FROM   [App_Pages]

WHERE [PageDescription] like 'Gestión Banca Premium'

 

SELECT  * FROM [BBIApps].[dbo].[App_Pages]

WHERE  [PageUrl] LIKE 'GestionBancaPremium/CreateEconomicGroup.aspx'

 

DECLARE @IdPage INT = 0

DECLARE @IdSubPage INT = 0

 

SELECT  @IdPage = IdPage

FROM   [App_Pages]

WHERE [PageDescription] like 'Gestión Banca Premium'

 

IF(@IdPage  = 0 )

BEGIN

                INSERT INTO [BBIApps].[dbo].[App_Pages] ([PageUrl],[PageDescription],[IdPageFather],[IdFather],[IdSon],[LoadApp],[UserLenguage])

                VALUES (NULL,'Gestión Banca Premium',1,1,1,0,'es')

                SET @IdPage = @@IDENTITY

END

PRINT @IdPage

 

 

SELECT @IdSubPage = IdPage FROM [BBIApps].[dbo].[App_Pages]

WHERE  [PageUrl] LIKE 'GestionBancaPremium/CreateEconomicGroup.aspx'

print @IdSubPage

IF(@IdSubPage  = 0 )

BEGIN

                INSERT INTO [BBIApps].[dbo].[App_Pages] ([PageUrl],[PageDescription],[IdPageFather],[IdFather],[IdSon],[LoadApp],[UserLenguage])

                SELECT T.*

                FROM (

                               SELECT 'GestionBancaPremium/CreateEconomicGroup.aspx' [PageUrl],'Grupo Económico' [PageDescription],@IdPage [IdPageFather],1 [IdFather],1 [IdSon],1 [LoadApp],'es' [UserLenguage]

                               ) T

                               LEFT OUTER JOIN [BBIApps].[dbo].[App_Pages]  L

                                               ON T.[IdPageFather] = L.[IdPageFather]

                --WHERE L.[IdPageFather] IS NULL

END

GO

 

SELECT  *

FROM   [App_Pages]

WHERE [PageDescription] like 'Gestión Banca Premium'

 

SELECT * FROM [BBIApps].[dbo].[App_Pages]

WHERE  [PageUrl] LIKE 'GestionBancaPremium/CreateEconomicGroup.aspx'
