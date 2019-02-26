#include <QCoreApplication>
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main(int argc, char *argv[])
{
    {
        std::vector<cv::Point2f> obj;
        std::vector<cv::Point2f> scene;
        std::vector<cv::Point2f> obj_projection;

        cv::Point2f A,B,C,D,A_P,B_P,C_P,D_P ;
        A.x=0;
        A.y=0;

        B.x=150;
        B.y=0;

        C.x=150;
        C.y=150;

        D.x=0;
        D.y=150;

        obj.push_back(A);
        obj.push_back(B);
        obj.push_back(C);
        obj.push_back(D);


        A_P.x=100;
        A_P.y=100;

        B_P.x=200;
        B_P.y=80;

        C_P.x=220;
        C_P.y=80;

        D_P.x=100;
        D_P.y=200;

        scene.push_back(A_P);
        scene.push_back(B_P);
        scene.push_back(C_P);
        scene.push_back(D_P);

        cv::Mat homography_matrix= cv::getPerspectiveTransform(obj,scene);
        std::cout<<"Estimated Homography Matrix is:" <<std::endl;
        std::cout<< homography_matrix <<std::endl;

        perspectiveTransform( obj, obj_projection, homography_matrix);
        for(std::size_t i=0;i<obj_projection.size();i++)
        {
            std::cout<<obj_projection.at(i).x <<"," <<obj_projection.at(i).y<<std::endl;
        }
    }
}
