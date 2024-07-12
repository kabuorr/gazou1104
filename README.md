import numpy as np
import cv2
import pathlib

def Log(img,k_size=(3,3),sigma=1.2):
    gauss_img=cv2.GaussianBlur(img,k_size,sigma)
    dst = cv2.Laplacian(gauss_img)
    return dst

def laplacian(img):
    kernel=np.array([[0,1,0],
                     [1,-4,1],
                     [0,1,0]])
    
    dst=cv2.filter2D(img,-1,kernel)
    return dst

if __name__ =='__main__':
    
    for i in range(10):
     src=cv2.imread("./img/ir0000(i).png")
    gray=cv2.cvtColor(src,cv2.COLOR_BAYER_BG2GRAY)
    #ファイルの画像を全て読み込む。
    dst=laplacian(gray)
    log=Log(gray)
    
    cv2.imshow("laplacian",dst)
    cv2.imwrite("./img/laplacian.png",dst)
    cv2.imshow("Log",log)
    cv2.imwrite("./img/log.png",log)

＃ラプラシアンフィルタとLogフィルタにかける
    
    cv2.waitKey(0)
