### Visual Code의 terminal에서 실행
1. git clone https://github.com/bcaitech1/p4-dkt-no_caffeine_no_gain
2. git config --global user.name "Anna-Lee"
3. git config --global user.email ceanna93@gmail.com
4. cd p4-dkt-no_caffeine_no_gain/
5. git checkout -b develop
6. git merge upstream/develop
7. git checkout -b anna/kfold
8. git status 
9. git add .(또는 특정 파일 이름)
10. git commit -m "업데이트/생성 파일..."
11. git push origin anna/kfold (또는 git push upstream)
12. git branch
14. git branch -D anna/kfold

- checkout: 작업하는 브랜치 경로를 옮기거나 -b를 통해 새로운 브랜치 생성
- branch -D \[브랜치명\]: PR 후에 merge가 완료되면(merge가 취소되더라도) branch를 삭제
