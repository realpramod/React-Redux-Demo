# React-Redux-Demo

on: [push]
jobs:
  build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v1
        - uses: azure/login@v1
          with:
                creds: ${{ secrets.AZURE_CREDENTIALS }}
        - uses: actions/checkout@v3
        - uses: azure/sql-action@v2.2.1
          with:        
            connection-string: ${{ secrets.AZURE_SQL_CONNECTION_STRING }}
            path: './DatabaseProjecttestdb/DatabaseProjecttestdb.sqlproj'
            action: 'publish'
            build-arguments: '-c Release'
            arguments: '/p:DropObjectsNotInSource=true' 

        - name: logout
          run: |
           az logout
                
