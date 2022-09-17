# Upload Maven packages to GitHub guide

>**If you don't want to deploy packages in your local environment, please check `.github/workflow/maven-publish.yml` file, GitHub Actions will auto trigger `build` and `deploy` command, and you can skip the below steps except step 2.** : )

1. Edit your ~/.m2/settings.xml  
    Please add below code block to your settings.xml file
    ```xml
    <servers>
        <server>
            <id>github</id>
            <username>${YOUR_GIT_ACCOUNT}</username>
            <password>${TOKEN}</password>
        </server>
    </servers>
    ```
    > How to generator your token
    > 1. GitHub settings
    > 2. Developer settings (The button of Tag List)
    > 3. Personal access tokens
    > 4. Generate new token
    > 5. Select all options you can see
    > 6. Then you can see your new token

2. Add the below code block to your repository `pom.xml`   
    1.  Add   
           ```xml
           <repository>xxx</repository>
           ```
        to your properties
     
    2.  ```xml
        <profile>
            <id>github</id>
            <repositories>
                <repository>
                    <id>central</id>
                    <url>https://repo1.maven.org/maven2</url>
                </repository>
                <repository>
                    <id>github</id>
                    <url>https://maven.pkg.github.com/${repository}</url>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
            </repositories>
        </profile>
        ```
   
3. ``mvn clean deploy`` should be successful
4. Finally, you can see the packages in your GitHub repository page as below pic
![img.png](img.png)
![img_1.png](img_1.png) 