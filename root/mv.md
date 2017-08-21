### mv

##### Issues

1. Argument list too long

    到所移动的文件夹下进行操作

        ls . | xargs -t -I {} mv {} target_path/{}
        ls . | xargs -t -I {} mv {} ../{}

1. 移动某文件夹下全部文件

        mv ./*
