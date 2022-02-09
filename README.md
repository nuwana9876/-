환경설정을 함에 있어서 저와 같이 힘들어하는 사람들을 위해, 제가 환경설정할 때, 어떻게 환경설정을 했는지를 글로 남깁니다.

해당내용은 windows에 pytorch를 사용하며, 그에 맞는 환경설정을 하는 방식을 다룹니다.

1. 기본적으로 anaconda 설치하면서 동시에 python 설치하는 것이 보통

   그러나 혹시 모르니까, base로 python 아무 버전이나 exe파일 실행해서 설치하자

2. 이후 anaconda를 설치했으면 (기본으로는 python 3.9 버전임. 이전버전을 깔고 싶으면 
 
   https://repo.anaconda.com/archive/에 들어가서 맞는 걸로 깔자) anaconda prompt를 실행

3. 명령어로 conda create -n (자기가 만들고 싶은 가상환경 이름) python = 3.x(python 버전)

   그리고 conda activate (가상환경 이름) (이건 앞으로 가상환경 실행할 때, 이 명령어를 사용한다)

4. 이후에 pytorch를 설치하고 싶지만 이전에 cuda와 cudnn을 버전에 맞게 설정해야한다.

5. nvcc --version or nvcc -V 라는 명령어를 치면 cuda의 버전을 볼 수 있다. 또한 nvidia-smi를 사용하면 내가 설치할 수 있는 cuda 버전을 볼 수 있다. 

   일단 처음 명령어(nvcc --version)를 쳤을 때 만약 오류가 뜨는 경우, 자신이 가지고 있는 gpu의 이름에 따라, 어떤 버전을 설치해야하는지 찾아야 한다. 이는 앞서 5번의 두번째 명령어인 nvidia-smi를 통해 CUDA Version이라고 쓰여있는 칸에 해당하는 버전이 최대 버전(추천 버전)이므로 이를 활용한다. (그것보다 더 큰 버전은 설치할 수 없을 것이다.)

6. 그럼 5번에서 알아낸 cuda 버전은 https://developer.nvidia.com/cuda-toolkit에서 설치가 가능하다. 만약 버전(최신 버전은 11.6)이 최신버전보다 이전의 버전을 설치해야하는 경우, 

   https://developer.nvidia.com/cuda-toolkit-archive 여기서 찾아서 설치하자.

   이렇게 한 후에, nvcc --version을 했을 때, 제대로 뜬다면 설치가 잘 된 것이라고 판단

   (여기서 window키 + S 하고 시스템 환경 변수 편집을 쳐서 환경변수로 들어가면 path를 알 수 있는데 path에 CUDA_PATH, CUDA_PATH Vx 가 없다면 수동으로 환경변수 편집해야한다.)

7. 다음으로 CuDNN을 설치하자. 이는 사용되는지는 알 수 없으나, CUDA의 성능을 올려주고 병렬처리가 좋아진다는 말을 들었으므로 같이 설치하는 게 좋다. 

   CUDA 버전을 확인하고, 그에 맞는 CuDNN을 설치해야한다. 

   대부분의 경우 최신버전까지는 설치하지 않으므로, 이전 버전의 cuDNN 사이트 https://developer.nvidia.com/rdp/cudnn-archive 를 이용해  

   내가 사용하고자 하는 cuda와 버전이 맞는 cuDNN을 다운받는다.

8. 자 거의 끝나간다. 이제는 pytorch를 설치할 시간이다. https://pytorch.org/ 에 들어가서 밑으로 내리면 pytorch를 어떻게 설치할지에 대한 설정을 하는 구간이 나오는데, 해당하는 것에 맞춰서 commend를 받아야한다. 


   나의 경우,conda를 이용한 설치였기에 conda,python,windows, cuda버전은 솔직히 잘 모르겠다. 
   
   나는 운이좋게도 추천하는 cuda 버전과 여기서의 cuda 11.3과 맞아서 설치했지만, 아마 cuda10, 11에 따라서 사용하면 될 것으로 예상된다.

9. 명령어를 anaconda prompt에 적어서 수행하면 된다. 그리고 이후에는 자신이 설치할 각종 라이브러리를 anaconda prompt에서 pip install 형태로 버전에 맞게 설치하면된다.

10. pycharm에 들어가서(이건 인터넷 치고 찾아서 설치하면 된다.) 설정을 다 마친 후,(이건 알아서 하세요) 
    
    python console창에 

    import torch

    torch.cuda.is_available() 이라는 코드를 쳤을 때, true가 뜬다면 당신은 gpu 설정을 잘 한 것이다.

    False라면, 솔직히 지우고 다시하고, 오류뜨면 고치는 수밖에 없다.

    대표적 오류는 import torch를 했을 때, 여기서 오류가 발생하는 경우이다.이는 한번 torch를 설치했다가 지우고 다시 까는 경우에 문제점으로 알고있다. 이에 대한 해결방안은 자신이 설치한 anaconda3 의 폴더를 찾아가, 자신이 설정한 가상환경 이름을 가진 폴더에 들어가고,
    
    이후 Lib->site-packages에서 torch라는 단어를 포함한 파일 모두를 삭제하는 것이다. 
    
    이후 재설치를 하게되면 아마 문제가 없거나 할 것이다. 

    물론 이거말고도 문제가 좀 많았지만, 잘 하실 수 있을거라 믿습니다.
