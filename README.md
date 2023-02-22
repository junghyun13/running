# running
V개의 마을와 E개의 도로로 구성되어 있는 도시가 있다. 마을에는 편의상 1번부터 V번까지 번호가 매겨져 있고 다음 E개의 줄에는 각각 세 개의 정수 a, b, c가 주어진다. a번 마을에서 b번 마을로 가는 거리가 c인 도로가 있고 일방통행이다.당신은 도로를 따라 운동을 하기 위한 경로를 찾으려고 한다. 운동을 한 후에는 다시 시작점으로 돌아오는 사이클을 찾는다. 사이클을 이루는 도로의 길이의 합이 최소로 하는 프로그램을 작성해보자!

#python
해결책은 플로이드와샬 알고리즘==> 모든정점에서 모든정점으로 최단경로를 구한다!!

import sys
inf=int(100000) #inf=int(1e9)로 해서 최댓값설정 할수도 있음 
v,e=map(int,sys.stdin.readline().split()) #v는 마을 e 도로
place=[[inf]*(v+1) for _ in range(v+1)]
for _ in range(e):
  a,b,c=map(int,sys.stdin.readline().split())
  place[a][b]=c
for q in range(1,v+1):
  for a in range(1,v+1):
    for b in range(1,v+1): #플로이드와샬 
      place[a][b]=min(place[a][b],place[a][q]+place[q][b])
answer=inf
for i in range(1,v+1):
  answer=min(answer,place[i][i])
if answer==inf:
  print(-1)
else:
  print(answer)

#c


#include <stdio.h>
#include <stdlib.h> 
#include <string.h>


int inf=1000,i,j;
int place[100][100];


void init(int v){
	for(i=1;i<=v;i++){
		for(j=1;j<=v;j++){
			if(j==i){
				place[i][j]=0;}
			else{
				place[i][j]=inf;}
		}}  }
		
		
int mincheck(int x,int y){ //최솟값찾기  
	return (x<y) ? x:y;  }


void main(){
	int a,b,c,v,e,q;
	scanf("%d %d",&v,&e);
	init(v);
	for(i=1;i<=e;i++){
		scanf("%d %d %d",&a,&b,&c);
		place[a][b]=c; }
	for(q=1;q<=v;q++){
		for(i=1;i<=v;i++){
			for(j=1;j<=v;j++){ //플로이드와샬->모든 정점에서 모든 정점으로 가는 최소 거리 구하기!
				place[i][j]=mincheck(place[i][j],place[i][q]+place[q][j]);}} }
	int answer=inf;
	for(i=1;i<=v;i++){
		for(j=1;j<=v;j++){
			if(j==i){
				continue;}
			if(place[i][j]!=inf && place[j][i]!=inf){ //자기 자신->자기 자신 마을로 돌아오는 거리 중 최솟값 구하기! 
			    answer=mincheck(answer,place[i][j]+place[j][i]);}} }
	if(answer==inf) printf("-1");
	else printf("운동을 최소한으로 하기 위한 사이클의 도로 길이의 합은: %d ",answer);  }
