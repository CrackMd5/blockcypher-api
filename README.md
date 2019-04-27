Recently I wrote a personal bitcoin payment system by c#. Others pay btc directly to my btc address. There is no need to go through other intermediate payment service providers. This system uses the api provided by www.blockchain.com and the api and webhooks provided by www.blockcypher.com. The c# api of www.blockchain.com can be found here:  https://github.com/CrackMd5/blockchain-api. 

 The following is the c# call method of webcyhooks of blockcypher.com.
 
Reference page:https://www.blockcypher.com/dev/bitcoin/#using-webhooks
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Text;
using System.Web.Helpers;

namespace webhooks
{
    public partial class WebForm1 : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            var mRead = Request.GetBufferedInputStream();
            byte[] Buf = new byte[12800];
            int count = mRead.Read(Buf, 0, 12800);
            string str = Encoding.UTF8.GetString(Buf, 0, count);
            dynamic JSON = Json.Decode(str);

            string txid = JSON.hash;
            int confirmations = JSON.confirmations;
            
            foreach (var o in JSON.outputs)
            {
                string addr = o.addresses[0];
                 int value = o.@value;
                 
                
            }
        }
    }
}
```


This bitcoin payament system has been applied on  my website: https://www.cmd5.org
