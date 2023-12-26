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
</td>

<td>

```swift
import SwiftUI
//用List來呈現disney的片單

struct Disney: Identifiable{
    var id = UUID()
    var image:String
    var DisneyNameUS:String //故事簡介
    var DisneyNameTW:String //中文片名
    var DisneyHours:String //上映時間
    var predict:String //預告片網址
}

var disney = [ //片單陣列
    Disney(image: "coco", DisneyNameUS: "故事講述一個名為米高·李維拉的11歲男孩意外穿越到亡靈的世界，他需要尋求自己的已故音樂家曾外祖父的幫助，把他送返現實世界", DisneyNameTW: "可可夜總會", DisneyHours: "2017/11/22", predict: "https://youtu.be/KtbCQDXiBdE?si=0RSIHfyC4u3SOBnU"),
    Disney(image: "brain", DisneyNameUS: "萊莉因為父親工作的因素舉家搬遷至舊金山，要準備適應新環境，但就在此時，萊莉腦中控制歡樂與憂傷的兩位腦內大臣- 樂樂與憂憂迷失在茫茫腦海中。\n大腦總部只剩下掌管憤怒、害怕與厭惡的三位幹部負責，導致本來樂觀的萊莉變成憤世嫉俗少女。樂樂與憂憂必須要盡快在複雜的腦中世界回到大腦總部，讓萊莉重拾原本快樂正常的情緒…。", DisneyNameTW: "腦筋急轉彎", DisneyHours: "2015/05/18", predict: "https://www.youtube.com/watch?v=1T_LbO3DqCM"),
    Disney(image: "brave", DisneyNameUS: "蘇格蘭高地擅使弓箭的公主梅莉達因為與母親艾琳諾皇后對未來的期盼產生分歧，發生爭執的過程意外導致母親被魔咒變成一頭熊，這使得梅莉達必須和艾琳諾皇后展開冒險，找出解除魔咒的方法。", DisneyNameTW: "勇敢傳說", DisneyHours: "2012/06/22", predict: "https://www.youtube.com/watch?v=UBiuNTx8wNk"),
    Disney(image: "frozen", DisneyNameUS: "擁有皇家血統的安娜被姊妹艾莎所詛咒，為解除詛咒，她與冒險的山民、馴鹿及雪人，一起踏上北上的路程...。", DisneyNameTW: "冰雪奇緣1", DisneyHours: "2013/12/27", predict: "https://www.youtube.com/watch?v=dQoR5WyfqQs"),
    Disney(image: "animal", DisneyNameUS: "在動物方城市裡，茶蒂哈普斯警官作為警隊里的第一任免子警官，下定決心證明自己。這就是為什麼她會抓住破案的機會，即使這意味著要和語速很快的狐狸騙子胡尼克合作來解開這個謎國。", DisneyNameTW: "動物方城市", DisneyHours: "2016/03/04", predict: "https://www.youtube.com/watch?v=v5ylDdPZm9A"),
    Disney(image: "sea", DisneyNameUS: "取材於太平洋島嶼玻里尼西亞文化流傳許久的毛伊半神人故事，主角莫娜的族人在島嶼上安居樂業，直到有一天，漁獲數量漸漸短少，而且農作物也減少產值，樹木慢慢枯死…莫娜的阿嬤告訴她一個神祕的傳說──大地之母本來擁有一顆海洋之心，但是卻被一位半神人毛伊取走，因此釋放了黑暗力量，生態的平衡受到了破壞，莫娜的使命則是找到半神人毛伊，請他歸還海洋之心，讓一切恢復原狀…。", DisneyNameTW: "海洋奇緣", DisneyHours: "2016/10/23", predict: "https://www.youtube.com/watch?v=0PjI4AyCEkw"),
    
]

struct DisneyListView: View {
    @State var showDetialView = false
    @State var selectedDisney: Disney?
    var body: some View {
        NavigationView{
            List(disney){DisneyItem in
                BasicImageRow(thisDisney : DisneyItem)
                    .onTapGesture {
                        self.showDetialView = true
                        self.selectedDisney = DisneyItem
                    }
            }
            .sheet(item: self.$selectedDisney, content: {DisneyItem in
                DisneyDetialView(thisDisney: DisneyItem)
            })
            .navigationTitle("迪士尼電影")
        }
    }
}

struct BasicImageRow: View {
    var thisDisney: Disney
    var body: some View {
        HStack{
            Image(thisDisney.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thisDisney.DisneyNameTW)
        }
    }
}

struct DisneyDetialView: View {
    @Environment(\.presentationMode)
    var presentationMode
    var thisDisney: Disney
    var body: some View {
        ScrollView{
            VStack{
                Image(thisDisney.image)
                    .resizable()
                    .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                    .clipped()
                Text(thisDisney.DisneyNameTW)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                Text("上映日期: " + thisDisney.DisneyHours)
                    .font(.caption)
                Spacer()
                Text(thisDisney.DisneyNameUS)
                    .padding(.all, 25)
                    .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                    .cornerRadius(30.0)
                    .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                    .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                Spacer()
                //使用Link的方式, 將youtube預告片的網址放進去
                Link("預告", destination: URL(string: thisDisney.predict)!)
                    .padding(.all,10)
                    .frame(width: 110, height: 45, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .font(.system(size: 30, design: .serif))
                    .cornerRadius(20)
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20) //後面留空多少空間
                    .padding(.top, 30)
                    Spacer()
                }
            }
        )
    }
}

```
  
</td>  

<td>

```swift
import SwiftUI
//用ScrollView來呈現動漫類的片單

struct Course: Identifiable{
    var id = UUID()
    var image:String
    var courseNameUS:String //故事簡介
    var courseNameTW:String //中文片名
    var courseHours:String //影片類型
    var predict:String //預告片
}

var courses = [
    Course(image: "king", courseNameUS: "「國王排名」是以麾下有名騎士的數量、國民人口、城鎮發展，以及國王本人是否像勇者一樣強大，綜合以上條件來評價各國國王的排行榜。「你想要成為全世界最棒的國王?」伯斯王國的大王子波吉，天生就聽不見、話也說不 好、身體孱弱得舉不起劍，即使如此，他仍然想完成與母親的約定。這樣的堅強與執著也感動了影子一族的卡克， 他決定支持波吉，並成為波吉第一個朋友!但波吉隔天卻怎麼找也找不到卡克。", courseNameTW: "國王排名", courseHours: "類型： 奇幻、冒險、勵志", predict: "https://www.youtube.com/watch?v=aqIJUjTzPbo"),
    Course(image: "spy", courseNameUS: "敘述一名身分為間諜的男性，和另一位實際工作是殺手的女性，以及一個能讀心的超能力者女孩，三人互相隱瞞真實身分所組成的虛假家庭間的家庭喜劇。", courseNameTW: "間諜家家酒", courseHours: "類型： 諜報動作、家庭喜劇", predict: "https://www.youtube.com/watch?v=l1uINfUshjc"),
    Course(image: "war", courseNameUS: "擁有超人般身體能力的男子高中生虎杖悠仁的故事。\n因為某種理由，想要每天17點之前回家的虎杖悠仁來到了不強制出席的靈異現象研究會，享受着悠閒的活動。這樣的某一天，來學校尋找被封印的詛咒之物的青年伏黑惠出現於虎杖的面前。", courseNameTW: "咒術迴戰", courseHours: "類型：  少年漫畫、黑暗奇幻、校園、戰鬥", predict: "https://www.youtube.com/watch?v=QH--l_kJ2lE"),
    Course(image: "kid", courseNameUS: "在演藝圈（這個世界）裏，謊言就是武器。\n在小城市工作的婦產科醫生吾郎，每天都過着與演藝圈無緣的生活。\n另一方面，他“推”的偶像“B小町”的愛開始登上明星之列。如此這般的兩人實現了“最糟糕”的相遇，從此命運的齒輪開始轉動…… ", courseNameTW: "我推的孩子", courseHours: "類型： 懸疑、偶像、戀愛", predict: "https://www.youtube.com/watch?v=ieGJ0CnGkLI"),
    Course(image: "shadow", courseNameUS: "在一個遙遠的地方，居住著一群假裝自己是貴族的人，因為他們沒有臉，必須仰賴被稱為臉的「活人偶」來互相交流，故事描述被稱為艾蜜莉可的臉與她的主人凱特在影宅中的奇妙生活，隨著她們的成長，影宅的神秘與黑暗也逐漸展現出來。", courseNameTW: "影宅", courseHours: "類型：  哥德式、神秘、超自然", predict: "https://www.youtube.com/watch?v=1QPhoqCzU_4"),
]

struct AnimeListView: View {
    @State var showDetialView = false
    @State var selectedAnime: Course?
    var body: some View {
        VStack{
            Text("Anime")
                .padding(.top, 20)
                .foregroundStyle(.secondary)
                .padding(.bottom, 0)
            Text("動漫類")
                .font(.system(size: 40, weight: .bold, design: .rounded))
                .padding(.all, 5)
            ScrollView(.horizontal){
                HStack{
                    ForEach(courses){CourseItem in
                        CardsView(image: CourseItem.image , courseNameUS: CourseItem.courseNameUS, courseNameTW: CourseItem.courseNameTW, courseHours: CourseItem.courseHours)
                            .frame(width: 300) 
                            .onTapGesture {
                                self.showDetialView = true
                                self.selectedAnime = CourseItem
                            }
                    }
                    .sheet(item: self.$selectedAnime, content: {CourseItem in
                        AnimeDetialView(thisAnime: CourseItem)
                    })
                }
            }
        }
    }
}

struct CardsView: View{
    var image:String
    var courseNameUS: String
    var courseNameTW: String
    var courseHours: String
    var body: some View{
        VStack{
            Image(image)
                .resizable()
                .aspectRatio(contentMode: .fit)
            VStack(alignment: .leading, content: {
                Text(courseNameTW)
                    .font(/*@START_MENU_TOKEN@*/.title/*@END_MENU_TOKEN@*/)
                    .foregroundStyle(.primary)
                    .lineLimit(3)
                Text(courseHours)
                    .font(.caption)
                    .foregroundStyle(Color(red: 0/255, green: 137/255, blue: 167/255))
            })
            .frame(minWidth: /*@START_MENU_TOKEN@*/0/*@END_MENU_TOKEN@*/, idealWidth: /*@START_MENU_TOKEN@*/100/*@END_MENU_TOKEN@*/, maxWidth: /*@START_MENU_TOKEN@*/.infinity/*@END_MENU_TOKEN@*/, alignment: .leading)
            .padding(.horizontal, 10)
            .padding(.bottom, 10)
        }
        .background(Color(red: 215/255, green: 240/255, blue: 187/255))
        .clipShape(.rect(cornerRadius: 20))
        .overlay(
            RoundedRectangle(cornerRadius: 20)
                .stroke(Color.gray, lineWidth: 2)
        )
        .padding(.all, 10)
        
    }
}

struct AnimeDetialView: View {
    @Environment(\.presentationMode)
    var presentationMode
    var thisAnime: Course
    var body: some View {
        ScrollView{
            VStack{
                Image(thisAnime.image)
                    .resizable()
                    .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                    .clipped()
                Text(thisAnime.courseNameTW)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                Text(thisAnime.courseHours)
                    .font(.caption)
                Spacer()
                Text(thisAnime.courseNameUS)
                    .padding(.all, 25)
                    .background(Color(red: 215/255, green: 240/255, blue: 187/255))
                    .cornerRadius(30.0)
                    .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                    .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                Spacer()
                //使用Link的方式, 將youtube預告片的網址放進去
                Link("預告", destination: URL(string: thisAnime.predict)!)
                    .padding(.all,10)
                    .frame(width: 110, height: 45, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .font(.system(size: 30, design: .serif))
                    .cornerRadius(20)
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20) //後面留空多少空間
                    .padding(.top, 30)
                    Spacer()
                }
            }
        )
    }
}


```  
</td>

  </tr>
</table>
