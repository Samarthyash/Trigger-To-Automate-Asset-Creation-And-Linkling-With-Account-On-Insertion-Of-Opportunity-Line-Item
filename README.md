public class OpportunityLineItemHandler {
  public static void IfProductCreatedSoAssetInsert(List<OpportunityLineItem> OpportunityLineItemList){
        Set<Id> OppIds = new Set<Id>();
        List<Asset> AssetList = new List<Asset>();
        for(OpportunityLineItem oppLine : OpportunityLineItemList){
            OppIds.add(oppLine.OpportunityId);
        }
        for(Opportunity opp : [SELECT Id ,Name, AccountId FROM Opportunity WHERE Id IN : OppIds]){
            Asset obj = new Asset();
            obj.Name = 'Demo '+ Opp.Name;
            obj.AccountId = opp.AccountId;
            AssetList.add(obj);
        }
        if(AssetList.size()>0){
            insert AssetList;
        }
    }
}
