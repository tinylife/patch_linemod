# patch linemod

## prerequisite

### pysixd

files: params/  pysixd/  t_less_toolkit/  tools/  
copied from [sixd_toolkit](https://github.com/thodan/sixd_toolkit)  
deal with model reading/rendering, datasets reading and evaluation  

### dataset

get dataset under top level folder folder using following cmd  
```
wget -r -np -nH --cut-dirs=1 -R index.html http://ptak.felk.cvut.cz/6DB/public/
```
### environment
ubuntu 16.04,anaconda 3.6(you can build with a lower version when high version can't work)
### library

install opencv3 with contrib rgbd module  
source:https://github.com/opencv/opencv/releases,  contrib module:https://github.com/opencv/opencv_contrib/releases
steps:Refer to https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html, build from source code,pay attention to debug with contrib module.

install pybind11  
source:https://github.com/pybind/pybind11/releases
reference:https://pybind11.readthedocs.io/en/master/

install open3d(for icp)
source:https://github.com/intel-isl/Open3D/releases,  you should download code under the Open3D-3rdparty file folder from https://github.com/intel-isl/Open3D-3rdparty
reference:http://www.open3d.org/docs/release/compilation.html 
in my environment,I didn't make open3d successfully,there are some errors in camera file,so I delete file under the camera before cmake, and I recover the file folder before make(or make install, I forget it)  
pip install -r requirements.txt

### steps

in target folder:  
mkdir build  
cd build/  
cmake ..  
make  

in top level folder, if use pybind:  
pip install target_folder/  

python patch_linemod_test.py
you should select train mode first,after train,you can choose test mode.
### how to evaluate

patch_linemod_test.py, 57-66, select dataset & mode, train & test  
tools/eval_calc_errors.py, 19-27, select dataset, run 
it will cost lots of memory,caculate one once if necessary.
tools/eval_loc.py, 180-186, select dataset, run  
Results are saved to top_level_folder/eval  

[Chinese blog](https://zhuanlan.zhihu.com/p/45538349)
