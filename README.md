#ERD T_SHOP


```mermaid

erDiagram
    USER {
        string id PK
        string email UK
        string password
        string firstName
        string lastName
        string phoneNumber
        datetime dateOfBirth
        datetime createdAt
        datetime updatedAt
        boolean isActive
        boolean emailVerified
        string avatarUrl
    }
    ADDRESS {
        string id PK
        string userId FK
        string street
        string city
        string state
        string country
        string zipCode
        boolean isDefault
        string addressType
    }
    ROLE {
        string id PK
        string name UK
        string description
    }
    PERMISSION {
        string id PK
        string name UK
        string description
        string category
    }
    USER_ROLE {
        string id PK
        string userId FK
        string roleId FK
        datetime assignedAt
    }
    ROLE_PERMISSION {
        string id PK
        string roleId FK
        string permissionId FK
    }
    CATEGORY {
        string id PK
        string name UK
        string description
        string slug UK
        string imageUrl
        int displayOrder
        string parentCategoryId FK
    }
    BRAND {
        string id PK
        string name UK
        string description
        string logoUrl
        datetime establishedYear
    }
    PRODUCT {
        string id PK
        string name
        string description
        string sku UK
        decimal price
        decimal comparePrice
        decimal cost
        int quantity
        string categoryId FK
        string brandId FK
        boolean isPublished
        boolean isFeatured
        datetime createdAt
        datetime updatedAt
    }
    PRODUCT_ATTRIBUTE {
        string id PK
        string productId FK
        string name
        string value
    }
    PRODUCT_IMAGE {
        string id PK
        string productId FK
        string imageUrl
        int displayOrder
        string altText
    }
    PRODUCT_VARIANT {
        string id PK
        string productId FK
        string sku UK
        decimal price
        decimal comparePrice
        int quantity
        string size
        string color
        string material
        string imageUrl
    }
    PRODUCT_REVIEW {
        string id PK
        string productId FK
        string userId FK
        int rating
        string comment
        datetime createdAt
        boolean isApproved
    }
    DISCOUNT {
        string id PK
        string code UK
        string description
        string discountType
        decimal value
        decimal minOrderAmount
        datetime startDate
        datetime endDate
        int usageLimit
        int usedCount
        boolean isActive
    }
    CART {
        string id PK
        string userId FK
        datetime createdAt
        datetime updatedAt
    }
    CART_ITEM {
        string id PK
        string cartId FK
        string productId FK
        string variantId FK
        int quantity
        datetime addedAt
    }
    ORDER {
        string id PK
        string userId FK
        string orderNumber UK
        string status
        decimal subtotal
        decimal tax
        decimal shippingCost
        decimal discount
        decimal total
        string shippingAddressId FK
        string billingAddressId FK
        string paymentMethod
        string paymentStatus
        string shippingMethod
        string trackingNumber
        datetime createdAt
        datetime updatedAt
    }
    ORDER_ITEM {
        string id PK
        string orderId FK
        string productId FK
        string variantId FK
        string productName
        string variantDetails
        decimal price
        int quantity
        decimal total
    }
    ORDER_HISTORY {
        string id PK
        string orderId FK
        string status
        string note
        datetime createdAt
    }
    PAYMENT {
        string id PK
        string orderId FK
        string transactionId UK
        decimal amount
        string paymentMethod
        string paymentStatus
        datetime paymentDate
        string paymentDetails
    }
    WISHLIST {
        string id PK
        string userId FK
        string name
        boolean isDefault
        datetime createdAt
    }
    WISHLIST_ITEM {
        string id PK
        string wishlistId FK
        string productId FK
        datetime addedAt
    }
    INVENTORY {
        string id PK
        string productId FK
        string variantId FK
        int quantity
        int reserved
        string location
        datetime lastUpdated
    }
    INVENTORY_HISTORY {
        string id PK
        string inventoryId FK
        int change
        string reason
        string referenceId
        datetime createdAt
    }
    SHIPPING_ZONE {
        string id PK
        string name
        string[] countries
        string[] states
        string[] zipCodes
    }
    SHIPPING_RATE {
        string id PK
        string zoneId FK
        string name
        decimal minOrderValue
        decimal maxOrderValue
        decimal rate
        boolean isActive
    }
    TAX_RATE {
        string id PK
        string country
        string state
        string zipCode
        decimal rate
        string taxName
        boolean isActive
    }
    NOTIFICATION {
        string id PK
        string userId FK
        string title
        string message
        string type
        boolean isRead
        datetime createdAt
    }
    USER ||--o{ ADDRESS : has
    USER ||--o{ ORDER : places
    USER ||--o{ CART : has
    USER ||--o{ WISHLIST : creates
    USER ||--o{ PRODUCT_REVIEW : writes
    USER ||--o{ USER_ROLE : assigned
    USER ||--o{ NOTIFICATION : receives
    ROLE ||--o{ USER_ROLE : assigned_to
    ROLE ||--o{ ROLE_PERMISSION : has
    ROLE_PERMISSION }o--|| PERMISSION : grants
    CATEGORY ||--o{ PRODUCT : contains
    CATEGORY ||--o{ CATEGORY : has_subcategories
    BRAND ||--o{ PRODUCT : manufactures
    PRODUCT ||--o{ PRODUCT_VARIANT : has
    PRODUCT ||--o{ PRODUCT_IMAGE : contains
    PRODUCT ||--o{ PRODUCT_ATTRIBUTE : has
    PRODUCT ||--o{ PRODUCT_REVIEW : receives
    PRODUCT ||--o{ CART_ITEM : added_to
    PRODUCT ||--o{ ORDER_ITEM : ordered_in
    PRODUCT ||--o{ WISHLIST_ITEM : saved_in
    PRODUCT ||--o{ INVENTORY : tracks
    PRODUCT_VARIANT }o--|| PRODUCT : belongs_to
    PRODUCT_VARIANT ||--o{ INVENTORY : tracks
    PRODUCT_VARIANT ||--o{ CART_ITEM : selected_in
    PRODUCT_VARIANT ||--o{ ORDER_ITEM : ordered_in
    CART ||--o{ CART_ITEM : contains
    CART }o--|| USER : belongs_to
    ORDER ||--o{ ORDER_ITEM : contains
    ORDER ||--o{ ORDER_HISTORY : has_history
    ORDER ||--o{ PAYMENT : has
    ORDER }o--|| USER : placed_by
    ORDER }o--|| ADDRESS : shipped_to
    ORDER }o--|| ADDRESS : billed_to
    DISCOUNT ||--o{ ORDER : applied_to
    WISHLIST ||--o{ WISHLIST_ITEM : contains
    WISHLIST }o--|| USER : created_by
    INVENTORY ||--o{ INVENTORY_HISTORY : has_history
    INVENTORY }o--|| PRODUCT : for_product
    INVENTORY }o--|| PRODUCT_VARIANT : for_variant
    SHIPPING_ZONE ||--o{ SHIPPING_RATE : has_rates
# ERD_TSHOP
```
