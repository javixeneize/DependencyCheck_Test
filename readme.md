
# Dependency check test

This project just tests the action. It does a checkout of the code to scan, builds a jar and runs dependency check against it. Then, it uploads the report as an artifact

A hello world would be needed to run this test. I suggest using something like https://github.com/hellokoding/springboot-jsp.git


Example:

on: [push]

jobs:
  depchecktest:
    runs-on: ubuntu-latest
    name: depecheck_test
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Build project with Maven
        run: mvn clean install
      - name: Depcheck
        uses: javixeneize/DependencyCheck_Action@main
        id: Depcheck
        with:
          project: 'test'
          path: '.'
          format: 'HTML'    
      - name: Upload Test results
        uses: actions/upload-artifact@master
        with:
           name: Depcheck report
           path: ${{github.workspace}}/reports
