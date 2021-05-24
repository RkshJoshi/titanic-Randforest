"#Titanic Dataset Analysis using Random forest" 


pd.cut is used to assign bins to continous featire. It helps to divide feature data in categories.
def simplify_ages(df):
    df['Age'] = df['Age'].fillna(-0.5)
    bins = (-1,0,5,12,18,25,35,60,120)
    group_names = ['Unknown','Baby','Child','Teenager','Student','Young Adult','Adult','Senior']
    categories = pd.cut(df['Age'], bins,labels=group_names)
    df['Age'] = categories
    return df
    
   Make scorer  will convert any loss function or evaluation parameter as scorer to utilize wih GridSearch CV or RandomSearchCV
   





Using KFOLD to make sure that predictions are right--
from sklearn.model_selection import KFold
def run_kfold(clf):
    kf =KFold(n_splits=10)
    outcomes = []
    fold = 0
    print(kf.get_n_splits(X_all))
    for train_index, test_index in kf.split(X_all):
        fold += 1
        X_train,X_test = X_all.values[train_index],X_all.values[test_index]
        y_train,y_test = y_all.values[train_index],y_all.values[test_index]
        clf.fit(X_train,y_train)
        pred = clf.predict(X_test)
        acc_score = accuracy_score(y_test,pred)
        outcomes.append(acc_score)
        print("Fold{} has accuracy of {}".format(fold,acc_score))
    print("Mean accuracy is",np.mean(outcomes))

run_kfold(clf)
