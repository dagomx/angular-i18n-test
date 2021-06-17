# InternationalizationTest

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 12.0.4.

This is an Angular i18n test.

Full tutorial: https://www.digitalocean.com/community/tutorials/angular-internationalization

### 1. Add Angular i18n module

    ng add @angular/localize

## 2. In the component add the i18n attribute. It may include meaning|description@@id


    <article>
      <h1 i18n="Card Header|Title for the under construction card@@constructionHeader">Under Construction!</h1>
      <p i18n="Card Descritpion|A description for the under construction card.@@constructionDescription">This page is under construction.</p>
    </article>

## 3. Update package.json with extract script

    "scripts": {
      "ng": "ng",
      "start": "ng serve",
      "start:es": "ng serve --configuration=es",
      "build": "ng build",
      "build:es": "ng build --configuration=es",
      "watch": "ng build --watch --configuration development",
      "test": "ng test",
      "extract": "ng xi18n --output-path src/locale"
    }

## 4. Run extract script. A new file will be created: src/locale/messages.xlf

    npm run extract

## 5. Copy src/locale/messages.xlf to src/locale/messages.es.xlf. In src/locale/messages.es.xlf add a <target> under each <source>  like this:

    <source>Under Construction!</source>
    <target>¡En construcción!</target>

## 6. Create spanish build. In angular.json file:

    {
      "projects": {
        "internationalization-test": {
          // ...
          "i18n": {
            "sourceLocale": "en-US",
            "locales": {
              "es": {
                "translation": "src/locale/messages.es.xlf",
                "baseHref": ""
              }
            }
          },
          "architect": {
            // ...
          }
        }},
      // ...
    }

## 7. In angular.json, create configuration settings for es under build:

    {
      "projects": {
        "internationalization-test": {
          // ...
          "architect": {
            "build": {
              // ...
              "configurations": {
                "production": {
                  // ...
                },
                "es": {
                  "localize": ["es"],
                  "outputPath": "dist/internationalization-test-es/",
                  "i18nMissingTranslation": "error"
                }
              }
            },
            // ...
          }
        }},
      // ...
    }

## 8. Update the configuration settings under serve

    {
      "projects": {
        "internationalization-test": {
          // ...
          "architect": {
            "serve": {
              // ...
              "configurations": {
                "production": {
                  "browserTarget": "internationalization-test:build:production"
                },
                "es": {
                  "browserTarget": "internationalization-test:build:es"
                }
              }
            },
            // ...
          }
        }},
      // ...
    }

## 9. Finally we can add a serve and build scripts in package.json

    {
      "scripts": {
        "ng": "ng",
        "start": "ng serve",
        "start:fr": "ng serve --configuration=es",
        "build": "ng build",
        "build:fr": "ng build --configuration=es",
        "test": "ng test",
        "lint": "ng lint",
        "e2e": "ng e2e",
        "i18n:extract": "ng xi18n --output-path src/locale"
      }
    }
