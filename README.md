# -
c language大作业框架
#include<graphics.h>
#include"easyx.h"
#include<stdio.h>
#include<stdlib.h>
#define HEIGHT 1080
#define WIDTH 1920
#define manu 1
#define game 2
#define pause 3
#define record 4

ExMessage msg;

int scene = manu;//初始菜单

void Draw_main(int scene)//绘制菜单
{
	IMAGE bkgraph,btgraph[3];
	switch(scene)
	{
	case manu://主菜单
		//RECT buttle[3];
		loadimage(&bkgraph, "graph//bk_main.jpg", WIDTH, HEIGHT);
		putimage(0, 0, &bkgraph);
			loadimage(&btgraph[0], "graph//button//start.png", 400, 100);
			loadimage(&btgraph[1], "graph//button//record.png", 400, 100);
			loadimage(&btgraph[2], "graph//button//drop out.png", 400, 100);
			for(int i=0;i<3;i++)
			{
				putimage(1.0 / 2 * WIDTH - 200, 1.0 / 2 * HEIGHT - 50 + i * 200,&btgraph[i]);
			}
			
		//solidrectangle(1.0 / 2 * WIDTH - 200, 1.0 / 2 * HEIGHT - 50+i*200, 1.0 / 2 * WIDTH + 200, 1.0 / 2 * HEIGHT + 50 + i * 200);
		break;
	case game://游戏进程
		loadimage(&bkgraph, "graph//grass.png", WIDTH, HEIGHT + 250);
		putimage(0, 0, &bkgraph);
		loadimage(&btgraph[0], "graph//quit.png", 32, 32);
		putimage(15, 15, &btgraph[0]);
		break;
	case record://榜单
		loadimage(&bkgraph, "graph//recordbk.jpg", WIDTH, HEIGHT);
		putimage(0, 0, &bkgraph);
		loadimage(&btgraph[0], "graph//quit.png", 32, 32);
		putimage(15, 15, &btgraph[0]);
		break;
	}
	
}

void event_list(ExMessage msg)
{
	switch (scene)
	{
	case manu:
		if ((msg.x > 1.0 / 2 * WIDTH - 200) && (msg.x < 1.0 / 2 * WIDTH + 200) && (msg.y >  1.0 / 2 * HEIGHT - 50) && (msg.y < 1.0 / 2 * HEIGHT + 50))
		{
			scene = game;
			Draw_main(scene);
		}
		if((msg.x > 1.0 / 2 * WIDTH - 200) && (msg.x < 1.0 / 2 * WIDTH + 200) && (msg.y > 1.0 / 2 * HEIGHT - 50+200) && (msg.y < 1.0 / 2 * HEIGHT + 50+200))
		{
			scene = record;
			Draw_main(scene);
		}
		if ((msg.x > 1.0 / 2 * WIDTH - 200) && (msg.x < 1.0 / 2 * WIDTH + 200) && (msg.y > 1.0 / 2 * HEIGHT - 50 + 400) && (msg.y < 1.0 / 2 * HEIGHT + 50 + 400))
		{
			exit(0);
		}
		break;
	case game:
		if ((msg.x > 15) && (msg.x < 42) && (msg.y > 15) && (msg.y < 42))
		{
			scene = manu;
			Draw_main(scene);
		}
		break;
	case record:
		if ((msg.x > 15) && (msg.x < 42) && (msg.y > 15) && (msg.y < 42))
		{
			scene = manu;
			Draw_main(scene);
		}
		break;
	}
}
void Date_process(int scene)
{
	if (scene == game)
	{

	}
}


int main()
{
	
	initgraph(WIDTH, HEIGHT,1);
	Draw_main(scene);


	while (1)
	{
		while (peekmessage(&msg))
		{
			switch (msg.message)
			{
			case WM_LBUTTONDOWN:
				event_list(msg);
				break;

			case WM_RBUTTONDOWN:
				break;

			}
		}
		Date_process()
	}

	closegraph();
	return 0;
}
