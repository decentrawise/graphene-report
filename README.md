This is an import script for getting Graphene transactions into the CoinTracking.info site.

[CoinTracking](https://cointracking.info) is a portfolio website for tracking cryptocurrency assets. They have lots of exchanges and blockchains already integrated with the site to import automatically. However, they do have a "Bulk CSV Import" option to add in data from different exchanges that don't have a dedicated import option.

This script uses the [`graphenejs`](https://github.com/decentrawise/graphenejs) library to make a connection to a Graphene blockchain, fetches all transactions for a given user, and converts it to a CSV file that can be imported into CoinTracking.

[![cc-by-sa](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

# Usage

This script requires Node to run; install Node locally and run:

```
yarn
yarn start myUsername [debug] [no_grouping] [op_type_filter]
```

Replace `myUsername` with the account username you wish to make a report for. Since Graphene data is completely open, there are no login credentials needed to get a full transaction report on any user.

The debug, no_grouping and op_type_filter parameters are optional.
`debug = true|false, default = false`
`no_grouping = true|false, default = false`
`op_type_filter = transfer, fill_order, etc, default=none`

Running the script will create a `{username}-transactions.csv` file in the `output` folder of the project. Head to the [CSV Import](https://cointracking.info/import/import_csv/) screen of CoinTracking (Enter Coins > Bulk Imports > CSV Import) and select that CSV file as the target.

## Automating multiple accounts

If you have several accounts you can copy `run_accounts_example.sh` to `run_accounts.sh` and input your desired accounts there as shown. Then run it using:
`./run_accounts.sh`

This will fetch data for all accounts and generate a file called `all-merged.csv` in the root folder. Instead of importing all the different files manually you can import this file directly in Cointracking as explained above.

# Caveats

An important limitation right now is that the API node used needs to be configured to store all operation history. That means setting the `max-ops-per-account` parameter in config.ini to a high value, I've used `max-ops-per-account = 200000` successfully for my own accounts. A replay of the blockchain is necessary after changing this parameter.
