```uml
@startuml

!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue
!define MAIN_ENTITY #MintCream-MistyRose


skinparam class {
    BackgroundColor Snow
    BorderColor Black
    ArrowColor Black
}

package "野菜ショッピングサイト" as target_system {

   entity "顧客マスタ" as customer <m_customers> <<M,MASTER_MARK_COLOR>> {
        + customer_code [PK]
        --
        pass
        name
        address
        tel
        mail
        del_flag
        reg_date
  
    }
    
    entity "購入テーブル" as purchase <d_purchase> <<T,TRANSACTION_MARK_COLOR>> {
        + order_id [PK]
        --
        customer_code [FK]
        purchase_date
        total_price
    }
    
    entity "購入詳細テーブル" as purchase_detail <d_purchase_detail> <<T,TRANSACTION_MARK_COLOR>> {
        + order_id [PK]
        + detail_id [PK]
        --
        item_code [FK]
        price
        num
    }
    
    entity "商品マスタ" as items <m_items> <<M,MASTER_MARK_COLOR>> {
        + item_code [PK]
        --
        item_name
        price
        category_id [FK]
        image
        detail
        del_flag
        reg_date
    }
    
    entity "カテゴリマスタ" as category <m_category> <<M,MASTER_MARK_COLOR>> {
        + category_id [PK]
        --
        name
        reg_items
    }
    
}

customer |o-ri-o{ purchase
purchase ||-ri-|{ purchase_detail
purchase_detail }-do-|| items
items }o-le-|| category

@enduml
```
