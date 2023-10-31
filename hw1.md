<h1>hw1</h1>
<table>
  <tr>
    <td>
      
```swift
      //我以懸賞單的形式，製作一頁是個人檔案
    
    import SwiftUI
    import UIKit
    
    struct ContentView: View {
        
        var body: some View {
            ZStack{//先用ZStack將背景和WANTED放進去
                Text("WANTED")
                    .frame(width: 360, height: 600, alignment: .top)
                    .background(Color(red: 255/255, green: 224/255, blue: 184/255))
                    .cornerRadius(10)
                    .fontWeight(.black)
                    .lineSpacing(20)
                    .font(.system(size: 75, design: .serif))
                    .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
                
                Rectangle()//照片外框用rectangle表示
                    .fill(Color(red: 71/255, green: 34/255, blue: 0/255))  
                    .frame(width: 330, height: 250)
                    .position(x: 192, y: 245)
                VStack{//用VStack將其他項目放進去
                    Image("yj")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 320, height: 160, alignment: .top)
                        .position(x: 192, y:205)
                    
                    Text("D E A D   O R   A L I V E")
                        .position(x: 192, y:290)
                        .fontWeight(.black)
                        .lineSpacing(20)
                        .font(.system(size: 30, design: .serif))
                        .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
                    
                    
                    Text("黃 昱 儒")//姓名
                        .position(x: 192, y:250)
                        .fontWeight(.black)
                        .lineSpacing(20)
                        .font(.system(size: 80, design: .serif))
                        .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
                    
                    
                    Image(systemName: "dollarsign")//我選的SF
                        .position(x: 50, y:220)
                        .fontWeight(.medium)
                        .font(.system(size: 50, design: .serif))
                        .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
                    
                    Text("   1103348-")//將學號當作是懸賞金額
                        .fontWeight(.bold)
                        .lineSpacing(20)
                        .font(.system(size: 50.0, design: .serif))
                        .position(x:192, y: 100)
                        .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
    //                    .font(.custom("Nagurigaki-Crayon",size: 50))
                    Text("你想活出怎樣的人生")//蒼鷺與少年中出現的書籍
                        .position(x: 192, y: 50)
                        .fontWeight(.black)
                        .lineSpacing(20)
                    
                        .font(.system(size: 30, design: .serif))
                        .foregroundColor(Color(red: 71/255, green: 34/255, blue: 0/255))
                }
            }.onAppear(perform: {
                let fontURL = Bundle.main.url(forResource: "crayon_1-1", withExtension: "ttf")! as CFURL
                CTFontManagerRegisterFontsForURL(fontURL, CTFontManagerScope.process, nil)
            })        
            .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
            .background(Color(red: 71/255, green: 34/255, blue: 0/255)) //在最後面放入咖啡色背景
        }
    }

```

<img width = "400"  src="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/IMG_0263.jpeg">
    </td>
  </tr>
</table>
