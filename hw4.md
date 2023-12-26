<h1>hw2</h1>
<table>
  <tr>
    <td>
      
```swift
import SwiftUI

struct ContentView: View {
    //將使用者的名字新增到頁面上
    @AppStorage("UserName") var UserName:String = ""
    
    var body: some View {
        VStack {
            Text("🤩推薦的片單🤩")
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
            HStack{
                Text("使用者: ")
                    .font(.system(size: 18))
                Text(UserName.isEmpty ?"" : UserName)
                    .font(.system(size: 18))    
            }
            TabView{
                Group{
                    WelcomeView()
                        .tabItem { 
                            Image(systemName: "rosette")
                            Text("Welcome")
                        }
                    DisneyListView()
                        .tabItem { 
                            Image(systemName: "list.bullet")
                            Text("Disney Movies")
                        }
                    AnimeListView()
                        .tabItem { 
                            Image(systemName: "film.stack.fill")
                            Text("Anime")
                        }
                    TaiwanListView()
                        .tabItem { 
                            Image(systemName: "play.square.stack")
                            Text("Taiwanese films")
                        }
                    CardView()
                        .tabItem { 
                            Image(systemName: "book")
                            Text("今天看什麼!!!")
                        }
                    progressView()
                        .tabItem { 
                            Image(systemName: "percent")   
                            Text("完成進度")
                        }
                    SettingView()
                        .tabItem { 
                            Image(systemName: "wrench.adjustable")
                            Text("settings")
                        }
                }
            }
        }.padding(.top, 20)
            .tint(Color(red: 160/255, green: 64/255, blue: 119/255)) //被點擊的TabItem顏色
            .onAppear(perform: {
                UITabBar.appearance().backgroundColor = UIColor(Color(red: 231/255, green: 209/255, blue: 224/255)) //TabView背景顏色
                
                UITabBar.appearance().unselectedItemTintColor = UIColor(Color(red: 52/255, green: 167/255, blue: 199/255))//沒被點擊的TabItem顏色
            })
            .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
            .background(Color(red: 231/255, green: 209/255, blue: 224/255))//APP背景顏色
    }
}


```
<img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/hw2_GIF.gif">
    </td>
    <td>
      
```swift
import SwiftUI
//首頁的畫面

struct WelcomeView: View {
    var body: some View {
        VStack {
            Image("film")
                .resizable()
                .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
               .frame(width: 340, height: 340, alignment: .center)
            Text("推薦給你💁🏻‍♀️\n看都看不完的好片")
                .font(.system(size: 40, weight: .bold, design: .rounded))
                .lineSpacing(10)
                .foregroundStyle(Color(red: 255/255, green: 145/255, blue: 25/255))
                .fontWeight(.heavy)
                .lineSpacing(10)
                .frame(width: 350, height: 150, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                .background(Color(red: 215/255, green: 240/255, blue: 187/255))
                .cornerRadius(30.0)
                .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                .multilineTextAlignment(.center)
            
        }.padding(.top, 20)
    }
}

```      
  </tr>
</table>
