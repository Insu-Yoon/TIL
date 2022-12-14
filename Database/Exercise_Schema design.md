# **Instagram 데이터베이스 스키마 디자인**

![image](https://user-images.githubusercontent.com/110891599/194301596-484b98e3-0e62-45ee-92a8-3961cea10ade.png)

## **고려한 사항**

-   게시물 작성 시 하나 이상의 이미지(image)를 올릴 수 있다.
-   이미지를 올릴 때, 사진을 설명하는 간단한 글(maintext)이 올라간다.
-   게시물 작성 시 해시태그(hashtag)를 남길 수 있으며, 같은 해시태그가 붙은 게시물을 모아서 볼 수 있다.
-   게시물에 좋아요를 누르거나, 댓글을 작성할 수 있다.
-   댓글을 작성하면, 작성자가 표시된다.
-   팔로워, 팔로잉 관계가 존재한다.

## **작성해 본 스키마**

![image](https://user-images.githubusercontent.com/110891599/194301608-b7339b4b-d574-4236-8421-2f51e4c8252e.png)


### **1:N 관계**

-   users와 comment : 한 명의 유저가 여러 개의 댓글을 남길 수 있다.
-   users와 followTable : 팔로워, 팔로잉을 테이블로 따로 작성하고, 해당 테이블과 users를 1:N 관계로 디자인했다.
-   users와 post : 한 명의 유저가 여러 개의 게시물을 작성할 수 있다.
-   post와 image : 하나의 게시물에 여러 개의 이미지를 업로드 할 수 있다.
-   post와 comment : 하나의 게시물에 여러개의 댓글이 작성될 수 있다.

### **N:M 관계**

-   users - likeTable - post : 한 명의 유저가 여러 게시물에 좋아요를 누를 수 있고, 한 게시물에 여러 명의 유저가 좋아요를 누를 수 있다. 
-   post - hashtagTable - hashtag : 하나의 게시물에 여러 개의 해시태그가 붙을 수 있고, 하나의 해시 태그가 여러 개의 게시물에 붙여질 수 있다.

N:M 관계는 Join 테이블을 작성하면 각각 1:N의 관계가 된다.
