# DavidCustomWebView

```
作者：程序员小冰 （转载请说明出处）博客地址：http://blog.csdn.net/qq_21376985

长期维护的Android项目，里面包括常用功能实现，以及知识点详解， 当然还有Java中的知识点。

具体请看github：https://github.com/QQ986945193/DavidAndroidProjectTools

```

今天带大家做一个可以下拉刷新的自定义WebView，首先先看一下我们今天要实现的效果:

![这里写图片描述](http://img.blog.csdn.net/20161020104006430)

当然我们这里也可以设置一下，不让它进行刷新的效果。不过刷新的话可以增加我们的美观性。

好了。我这里先给大家看一下使用的方法：

```
package davidcustomwebview.qq986945193.com.davidcustomwebview;

import android.app.Activity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.widget.CompoundButton;
import android.widget.ToggleButton;


/**
 * @author ：程序员小冰
 * @新浪微博 ：http://weibo.com/mcxiaobing
 * @GitHub: https://github.com/QQ986945193
 * @CSDN博客: http://blog.csdn.net/qq_21376985
 */

/**
 * 自定义WebView支持下拉刷新的功能
 */
public class DavidWebViewActivity extends Activity {

    /**
     * 若是需要设置一下功能 可在DavidWebView中进行设置
     */
    private DavidWebView davidWebView;
    private ToggleButton tb;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_david_webview);
        davidWebView = (DavidWebView) findViewById(R.id.davidWebView);
        tb = (ToggleButton) findViewById(R.id.tb);
        initData();

    }


    protected void initData() {
        davidWebView.setOnRefreshWebViewListener(new OnRefreshWebViewListener() {
            @Override
            public void onRefresh() {
                // 模拟接口调用3秒
                new Handler() {
                    @Override
                    public void handleMessage(Message msg) {
                        //调用接口结束
                        davidWebView.setRefreshSuccess();
//                        davidWebView.setRefreshFail();
                    }
                }.sendEmptyMessageDelayed(0, 3000);
            }
        });

        davidWebView.getWebView().loadUrl("http://blog.csdn.net/qq_21376985");
        tb.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if (isChecked) {
                    //支持刷新
                    davidWebView.setRefreshEnable(true);
                } else {
                    //不支持刷新
                    davidWebView.setRefreshEnable(false);
                }
            }
        });
    }
}

```

刷新的话调用setOnRefreshWebViewListener()方法即可。控制是否可以刷新，只需调用它的

setRefreshEnable()方法，进行判断。使用起来是不是很简单呢？不过里面有一些自定义的webview,

大家把里面的类与布局资源文件拷贝到自己的项目中，直接按上面的方法调用即可。

所以考虑到还有好多布局文件，所以，我这里就不给大家一一来写了。如果感兴趣的话，

可以自行下载源代码，进行优化，美化。使用。研究。。。。。。
