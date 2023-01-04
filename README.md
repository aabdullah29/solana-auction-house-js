# Auction House [link](https://docs.metaplex.com/programs/auction-house/)
- Creating an Auction House
- Listing and Bidding
- Executing a Sale
- Auctioning Fungible Assets
- Buying asset using a custom SPL Token
- Custom Order Matching
- Auctioneer


# JavaScript SDK

- Creating and updating the Auction House
    ```
    metaplex.auctionHouse().create();
    metaplex.auctionHouse().update();
    ```

- Trading on Auction House
    ```
    metaplex.auctionHouse().bid();
    metaplex.auctionHouse().list();
    metaplex.auctionHouse().executeSale();
    ```

- Cancelling a bid or listing
    ```
    metaplex.auctionHouse().cancelBid();
    metaplex.auctionHouse().cancelListing();
    ```

- Finding bids, listings and purchases
    ```
    metaplex.auctionHouse().findBidBy();
    metaplex.auctionHouse().findBidByTradeState();
    metaplex.auctionHouse().findListingsBy();
    metaplex.auctionHouse().findListingByTradeState();
    metaplex.auctionHouse().findPurchasesBy();
    ```

# Auction House Settings
- The Authority
- Trade Settings
    - treasuryMint
    - sellerFeeBasisPoints
- Helper Accounts
    - auctionHouseFeeAccount
    - auctionHouseTreasury
    - feeWithdrawalDestination
    - treasuryWithdrawalDestination
- Require Sign Off
- Can Change Sale Price
- Auctioneer Settings
    - hasAuctioneer
    - auctioneerAuthority
    - auctioneerScopes



# Managing Auction Houses
- Create Auction Houses
- Auction House Account
    ```
    const { auctionHouse } = await metaplex.auctionHouse().create({...});
    auctionHouse.address;                   // The public key of the Auction House account              
    auctionHouse.auctionHouseFeeAccount;    // The public key of the Auction House Fee account
    auctionHouse.feeWithdrawalDestination;  // The public key of the account to withdraw funds from Auction House fee account
    auctionHouse.treasuryMint;              // The mint address of the token to be used as the Auction House currency
    auctionHouse.authority;                 // The public key of the Auction House authority
    auctionHouse.creator;                   // The public key of the account used to create the Auction House instance
    auctionHouse.bump;                      // The `Bump` of the Auction House instance
    auctionHouse.feePayerBump;              // The `Bump` of the fee account
    auctionHouse.treasuryBump;              // The `Bump` of the treasury account
    auctionHouse.auctioneerAddress;         // he public key of the `Auctioneer` account
    ```


- Fetch Auction Houses
    - By address
    - By creator and mint
- Update Settings
    ```
    const updatedAuctionHouse = await metaplex
        .auctionHouse()
        .update({
            auctionHouse,
            authority: currentAuthority,
            newAuthority: newAuthority.address,
            sellerFeeBasisPoints: 100,
            requiresSignOff: true,
            canChangeSalePrice: true,
            feeWithdrawalDestination: newFeeWithdrawalDestination,
            treasuryWithdrawalDestination: newTreasuryWithdrawalDestination
        });
    ```

- Withdraw Funds
    - Auction House Fee Wallet to the Fee Withdrawal Destination Wallet
    - Transfers funds from Auction House Treasury Wallet to the Treasury Withdrawal Destination Wallet


# Trading Assets on Auction House
- Listing assets
    - Listing at price greater than 0
    - Listing at price of 0
    - In case of Non-Fungible Tokens (NFTs)
    - In case of Fungible Assets


- Bidding on assets
    - Private bids
    - Public bids
    - Partial Buy Order
    - Complete Buy Order

- Executing sale of assets
    - The Auction House transfers the bid amount from the buyer escrow account to the seller's wallet
    - The Auction House transfers the asset from the seller's wallet to the buyer's wallet
    - Direct Buy
    - Direct Sell
    - Independant Sale Execution

- Cancel Listings and Bids
    ```
    const listing = await metaplex
        .auctionHouse()
        .findListingByReceipt({...}) // we will see how to fetch listings in the coming pages
        
    const bid = await metaplex
        .auctionHouse()
        .findBidByReceipt({...})     // we will see how to fetch bids in the coming pages
        
    // Cancel a bid
    const cancelBidResponse = await metaplex               
        .auctionHouse()
        .cancelBid({
            auctionHouse,            // The Auction House in which to cancel Bid
            bid: bid,                // The Bid to cancel
        });

    // Cancel a listing
    const cancelListingResponse = await metaplex
        .auctionHouse()
        .cancelListing({
            auctionHouse,            // The Auction House in which to cancel listing
            listing: listing,        // The listing to cancel
        });
    ```


# Managing Buyer Escrow Account
- Getting Balance
- Deposit Funds
- Withdraw Funds

# Auction House Receipts
- Printing Receipts
    - PrintListingReceipt
    - PrintBidReceipt
    - PrintPurchaseReceipt
    - CancelListingReceipt
    - CancelBidReceipt
    - printReceipt
    - bookkeeper


# Finding bids, listings and sales
- Find all in an auction house
    - Find all bids in an Auction House
    - Find bids by buyer and mint
    - Find bids by metadata
    - Find all listings in an Auction House
    - Find listings by seller and mint
    - Find all purchases in an Auction House
    - Find purchases by buyer and mint
    - Find purchases by metadata
    - Find purchases by seller and buyer

- Find by receipt
    - Find a bid by receipt
    - Find a listing by receipt
    - Find a sale / purchase by receipt

- Find by trade state
    - Find a bid by trade state
    - Find a listing by trade state
    - Find a sale / purchase by trade state


