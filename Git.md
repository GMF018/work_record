## git

  ### 一、配置 user.name 和email

  ```shell
  git config --global user.name 'gmf'
  git config --global user.email '727244343@qq.com'
  ```

  ### 二、检查是否存在SSH key

  ```shell
  cd ~/.ssh
  ls 或 ll
  #查看是否粗在 id_rsa 和 id_rsa.pub 文件，如果存在，则说明已经有SSH key
  
  ```

  ### 三、生成SSH key

  ```shell
  ssh-keygen -t rsa -C '727244343@qq.com'
  ```

  ### 四、获取SSH key

  ```shell
  cat id_rsa.pub 
  ```

  ### 五、添加SSH Key

  ```shell
  github/ Settings/SSH and GPG keys
  ```

  ### 六、验证和修改

  ```shell
  ssh -T git@github.com
  ​```
  ```

  

  
