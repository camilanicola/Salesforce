## Data Factory

`public class TestDataFactory {//criação de dados para teste (só obj nativos e campos nativos obrigatórios)`

`public static Profile perfilNovo(){
        Profile p = new Profile();
		p.Name='System Administrator';
        Id pId = [select id from Profile LIMIT 1].Id;
        system.debug('Id '+ pId);
        p.id=pId;
        return p;
    }`	

`public static User usuarioTeste(id profileName){//criação do usuario teste`

        userRole role= new userRole(DeveloperName='TestRole', Name='Test Role'); //criação de role  
        insert role;
        
        User u = new User(//criação do novo usuário com os campos necessários
        ProfileId=profileName,
        LastName ='last',
        Email ='emailDeTeste@teste.com',
        Username ='Teste@teste.com',
        CompanyName='EmpresaTeste',
        Title='Sales Person',
        Alias = 'alias',
        TimeZoneSidKey = 'America/Los_Angeles',
        EmailEncodingKey = 'UTF-8',
        LanguageLocaleKey = 'en_US',
        LocaleSidKey = 'en_US',
        UserRoleId = role.Id
        );
        
        return u; `
        }
        public static Lead leadTeste(){
        Lead lead = new Lead(CNPJ_ou_CPF__c='47960950000121',
                             LastName='Nicola',
                            Company='Magalu');
        return lead;
        
    }
        public static Account contaTeste(id usuario){
            
            Account conta = new Account();
                       
            conta.Name = 'Conta ';
            conta.AccountNumber='001';
            conta.CurrencyIsoCode='USD';
            conta.OwnerId=usuario;
         
          return conta;
        }
        public static Contact contatoPrincipal(Id idConta){
            //pra criar mais é só criar uma lista e rodar um for aqui 			//dentro
            Contact contato= new Contact();
                    
            contato.LastName='Teste';
            contato.FirstName='Chihiro';
            contato.AccountId=IdConta;
            contato.CurrencyIsoCode='USD';
            contato.Email = 'test@gmail.com';
                         
            return contato;
        }
         public static Opportunity oppTeste (Id idConta){
            
            Date closeDate = System.TODAY().addYears(1);//a opp vence em 1 ano
          
             Opportunity opp = new Opportunity(); 
              
             opp.Name ='Oportunidade Teste';
             opp.AccountId = idConta;
             opp.StageName='Negotiation';
             opp.CloseDate= closeDate;
             
            return opp;      
        }
        public static Product2 prodTeste(){
            Product2 prdt = new Product2(
                    Name='Produto Teste', 
                   	IsActive = true);
            return prdt;
        }
        public static Pricebook2 prbTeste (){
            Pricebook2 standardPricebook = new Pricebook2();
            standardPricebook.IsActive = true;
            standardPricebook.Id = Test.getStandardPricebookId();
            update standardPricebook;
             return standardPricebook;            
        }
        public static PricebookEntry pbeTeste(Id standardPricebook, Id prod){
            PricebookEntry pbe = new PricebookEntry();
                pbe.Product2Id = prod;
                pbe.Pricebook2Id = standardPricebook;
                pbe.UnitPrice = 1.00;
                pbe.IsActive = true;
               return pbe;
        }
        public static Quote qtTeste(Id opp,id acc,id standardPricebook){
            Quote qt = new Quote();            
                qt.OpportunityId = opp;
                qt.Name = 'Test Accepted Quote';
                qt.Pricebook2Id = standardPricebook;
         
                return qt; 
        }
        public static QuoteLineItem qliTeste(id qt,id prdt,id pbe){
            QuoteLineItem qli = new QuoteLineItem();
                qli.QuoteId = qt;
                qli.Product2Id = prdt;
                qli.PricebookEntryId = pbe;
                qli.UnitPrice = 1;
                qli.Quantity = 1;
                
                return qli;
        }
        public static Order ord(id acc,id standardPricebook){
             Order ord = new Order();
                ord.AccountId = acc;
                ord.Status = 'Draft';
                ord.EffectiveDate = Date.today();
                ord.Pricebook2Id = standardPricebook;
                
                return ord;
        }
        public static OrderItem oli(id prdt,id ord,id pbe){
            OrderItem oli = new OrderItem();  
                oli.Product2Id = prdt;
                oli.Quantity = 1;
                oli.OrderId = ord;
                oli.PricebookEntryId = pbe;
                oli.UnitPrice = 1;
                
                
                return oli;
        }
        public static Contract ctr(id acc,id profile,id standardPricebook){
       	Contract ctr = new Contract();
           
           ctr.AccountId=acc;
           ctr.OwnerId=profile;
           ctr.StartDate=Date.today();//o contrato começa no dia da criação
           ctr.Status='Draft';
           ctr.Cliente_entrega__c=acc;
           ctr.EndDate=Date.today()+30;//fim do contrato ocorre em 30 dias
           ctr.Pricebook2Id=standardPricebook;
         return ctr;
       }
       public static EmailTemplate emtTeste(){
            EmailTemplate emt = new EmailTemplate();
            	emt.Name = 'Email Test';
                emt.HtmlValue = '<messaging:emailTemplate subject="Your Idea has been created"> </messaging:emailTemplate>';
                emt.DeveloperName = 'test';
                emt.FolderId = UserInfo.getUserId();
                emt.TemplateType = 'text';
                emt.IsActive = true;
            return emt;
        }    
`}`
